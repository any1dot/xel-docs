# Start the xel\_miner

In this tutorial, we want to demonstrate how to use the miner to actually work on tasks on the XEL blockchain. We will not go through every tiny little function of the miner \(this is something for a future article\), yet we will cover everything you need to know to get started mining.

## **Prerequisites \(optional\)**

Before you get started, you have to decide whether you want to use the miner remotely, or if you want to mine through a local node. In the case of Xeline, it is absolutely fine to use a remote wallet, since the signing is done locally, and your private key never leaves your computer. This is different in the case of the miner: when submitting proof-of-work results or solution candidates, your private key is submitted to the server as well, since the miner, as of now, has no logic to sign transactions built in. We hope that this will change in the future.

So the safest bet is to set up a local XEL node on your system. Before you do so, you have to make sure that you have a working Docker installation and that docker is fully functional on your computer. There are thousands of guides on how to do it for all different kinds of platforms.

In a next step, you have to clone the XEL docker repository:

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
git clone https://github.com/OrdinaryDude/xel-docker.git
```
{% endcode-tabs-item %}
{% endcode-tabs %}

If you are on a windows system, you can use [TortoiseGit](https://tortoisegit.org/download/) or just download the .zip archive at:

{% code-tabs %}
{% code-tabs-item title="\#link" %}
```http
https://github.com/OrdinaryDude/xel-docker/archive/master.zip
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Now, go into the `xel_docker` directory and launch

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
docker build -t xel .
```
{% endcode-tabs-item %}
{% endcode-tabs %}

If something goes wrong, you probably do not have the docker executable in your PATH – you might want to double check this. After a few minutes of waiting, your XEL docker image should be ready. If you are on a linux of macOS machine, launching the node is fairly simple. Just use the following bash script:

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
./run_with_computation.sh
```
{% endcode-tabs-item %}
{% endcode-tabs %}

If you are on Windows, launch it by using Docker directly instead. Make sure you launch this command from within the xel-docker/ directory.

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
docker run -p 17876:17876 -p 17874:17874 -p 16876:16876 -p 16874:16874 --mount type=bind,source=xel_data_dir,target=/elastic-core-maven/nxt_test_db --mount type=bind,source=conf,target=/elastic-core-maven/conf_user -i -t xel
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Now, you have to give the node some time. You want it to synchronize the blockchain entirely before you proceed. Maybe it’s time for an extended walk, a coffee or just a short break.

## **Installing the Miner**

The installation of the miner is [covered in our article on how to become a master at ePL](https://xeline.org/programming-in-epl). If you haven’t done so, please follow the installation instructions over there.

## **Using the Miner**

Once you are in the directory where your xel\_miner executable is, its a good start to take a look at the help information xel\_miner provides:

On linux and on macOS, that would be

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
./xel_miner --help
```
{% endcode-tabs-item %}
{% endcode-tabs %}

On Windows

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
xel_miner.exe --help
```
{% endcode-tabs-item %}
{% endcode-tabs %}

In the remainder of this tutorial, we will just cover the linux/macOS variant but the Windows one should be always analogous to that. After you have launched that command you will see the help:

{% code-tabs %}
{% code-tabs-item title="\#output" %}
```c
** Elastic Compute Engine **
   Miner Version: 0.9.6
   ElasticPL Version: 0.9.4
Usage: xel_miner [OPTIONS]
Options:
  -c, --config          Use JSON-formated configuration file
      --deadswitch   Hardkill the instance after x seconds
  -D, --debug                 Display debug output
      --debug-epl             Display EPL source code
  -d, --delaysleep	     	  Sleep x seconds after submitting POW: useful for burstless debugging
   -i, --ignoremask			  Debug only: ignore 0=nothing, 1=PoW, 2=Bty, 3=Both
   -h, --help                 Display this help text and exit
  -m, --mining PREF[:ID]      Mining preference for choosing work
                                profit       (Default) Estimate most profitable based on POW Reward / WCET
                                wcet         Fewest cycles required by work item
                                workid		 Specify work ID
      --no-color              Don't display colored output
      --opencl	              Run VM using compiled OpenCL code
      --opencl-gthreads    Max Num of Global Threads (256 - 10240, default: 1024)
      --opencl-vwidth 	  Vector width of local work size (1 - 256, default: calculated)
  -o, --url=URL               URL of mining server
  -p, --pass        Password for mining server
  -P, --phrase    Secret Passphrase for Elastic account
      --protocol              Display dump of protocol-level activities
  -q, --quiet                 Display minimal output
  -r, --retries            Number of times to retry if a network call fails
                              (Default: Retry indefinitely)
  -R, --retry-pause        Time to pause between retries (Default: 10 sec)
  -s, --scan-time          Max time to scan work before requesting new work (Default: 60 sec)
  	  --test-miner      Run the Miner using JSON formatted work in 
      --test-vm         Run the Parser / Compiler using the ElasticPL source code in 
	  --test-avoidcache   	  Do not save metadata
      --test-block 	  Block-id for test run
	  --test-cont-bounty      Search for bounties within test-vm environment
	  --test-cont-pow         Search for proof-of-work within test-vm environment
	  --test-work 	  Work-id for test run
	  --test-limit-storage 			Only allow storage sizes up to 
	  --test-multiplicator <32-byte-hex>	Multiplicator for testrun: must be exactly 32 hex chars
	  --test-publickey <32-byte-hex>		Publickey for testrun: must be exactly 32 hex chars
	  --test-stdin		                    Read storage values from stdin
	  --test-target <16-byte-hex>		    Target for test run: must be exactly 16 hex chars
	  --test-wcet-main 		Do not ignore WCET limits of main function in Test-Vm run
	  --test-wcet-verify 	Do not ignore WCET limits of verify function in Test-Vm run
  -t, --threads            Number of miner threads (Default: Number of CPUs)
  -u, --user        Username for mining server
  -T, --timeout            Timeout for rpc calls (Default: 30 sec)
      --validate              Validate logic in 'main' & 'verify' functions
	  --verify-only           Use verify instead of main
  -v, --version               Display version information and exit
  -X  --no-renice             Do not lower the priority of miner threads
Options while mining ----------------------------------------------------------

   s +                 Display mining summary
   d +                 Toggle Debug mode
   q +                 Toggle Quite mode
```
{% endcode-tabs-item %}
{% endcode-tabs %}

We will not cover all options in this tutorial, only those which are required to get your miner ready to work on tasks on the XEL Blockchain. First of all, we want to take a look at the threads configuration parameter:

{% code-tabs %}
{% code-tabs-item title="\#info" %}
```bash
-t, --threads            Number of miner threads (Default: Number of CPUs)
```
{% endcode-tabs-item %}
{% endcode-tabs %}

This parameter allows you to configure how many threads you want xel\_miner to run on. The more threads you use, the faster xel\_miner will find solutions. However, if you set this number too high your system may become unresponsive.

The next parameter we want to look at is the url configuration:

{% code-tabs %}
{% code-tabs-item title="\#info" %}
```bash
-o, --url=URL               URL of mining server
```
{% endcode-tabs-item %}
{% endcode-tabs %}

This allows you to point the miner to either a remote node or a local node. Either way is fine, but keep in mind that remote URLs do leak your private key to the server at the moment. If you do not trust the remote node, stick to a local one instead. The URL is always given in the form of `http://hostname:port` where `hostname` is the IP or FQDN of the host, and `port` is either `17876` for the mainnet or `16876` for the testnet.

The third important parameter is the passphrase flag:

{% code-tabs %}
{% code-tabs-item title="\#info" %}
```bash
-P, --phrase    Secret Passphrase for Elastic account
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="warning" %}
This is absolutely essential. 
{% endhint %}

This is the passphrase to the account which will both pay the transactions fees for submitting work results and receive the rewards in exchange. if your passphrase has a space in it, make sure to put double quotes around it. 

{% hint style="info" %}
It is absolutely essential that you have some initial funds inside this account, otherwise you will not be able to submit any solutions. 
{% endhint %}

For testing purposes you can just use your 12 word Xeline mnemonic code \(enclosed in double quotes\) since it’s very easy to get some XEL from the faucet to get started.

Now, for this tutorial, we want to launch a miner running just one thread, mining via our local node on the testnet. Hence, we start it like this:

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
./xel_miner -t 1 -o http://localhost:16876 -P "our twelve word passphrase goes here"
```
{% endcode-tabs-item %}
{% endcode-tabs %}

If you really prefer using one of the public nodes, feel free to use once of the balancer nodes instead:

{% code-tabs %}
{% code-tabs-item title="\#run" %}
```bash
./xel_miner -t 1 -o http://balance-1.xel.org:16876 -P "our twelve word passphrase goes here"
```
{% endcode-tabs-item %}
{% endcode-tabs %}

When there is no work on the network, you should see something like this:

![](https://xeline.org/wp-content/uploads/2018/04/Screen-Shot-2018-04-20-at-7.08.26-pm-1024x598.png)

If this is the case, you should maybe work through one of the other tutorials and post some work to the Blockchain. If you have done so, you should see the miner pick up on your work pretty quickly:

![](https://xeline.org/wp-content/uploads/2018/04/Screen-Shot-2018-04-20-at-7.14.50-pm.png)

At this point, your miner is already solving proof-of-work packages and submitting bounties / solutions to algorithms for which it has found solutions. Let us take a look at one little anomaly here.

You have probably noticed these lines:

{% code-tabs %}
{% code-tabs-item title="\#output" %}
```c
[19:15:27] CPU0: ***** POW limit reached for this block, pausing until next block *****
[19:15:43] CPU0: ***** Bounty limit reached for this block, pausing until next block *****
```
{% endcode-tabs-item %}
{% endcode-tabs %}

The first line means that the maximum number of allowed POWs for this block has already been reached in the unconfirmed transaction cache and there is no need to submit more until the next block arrives. We already know, that the retargeting algorithm tries to calibrate the target value so that 10 proof-of-work submissions \(on average\) are found per minute. This is not per task but for all tasks in the network together. However, as a DOS precaution, there is a hard cap of 25 proof-of-work submissions per block. Once that number is reached, no more proof-of-work submissions are accepted until the next block is found.

The bounty limit behaves similarly. In this scenario we have a job that takes one bounty per iteration and runs for three iterations. Since one iteration corresponds to as least one full block, there is no need to submit more than one bounty per block. So once a bounty has been found \(in this case, this can be more for other tasks\), we have to wait until the iteration count increases by one in the next block.

{% hint style="info" %}
You do not need to continuously monitor the console output. If you launch Xeline, you can see a few basic mining statistics in the left sidebar:
{% endhint %}

![](https://xeline.org/wp-content/uploads/2018/04/Screen-Shot-2018-04-20-at-8.00.04-pm-300x244.png)

Now, you are ready and set to start mining – be it your own tasks for testing purposes or other tasks for some XEL in exchange.

{% page-ref page="../../elastic\_pl/epl/" %}

>

