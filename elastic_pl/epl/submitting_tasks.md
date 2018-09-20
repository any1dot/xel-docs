# ePL – Submitting Tasks

It Is Time to Submit Your Task to the Blockchain. Before you do so, we strongly recommend that you read and understand the guide found [here](https://xeline.org/programming-in-epl). We will be reusing this example in this guide. The difference is, while we were testing the code just locally in the previous guide, we will submit that task to the XEL Blockchain.

## **Getting Xeline Ready**

![](https://xeline.org/wp-content/uploads/2018/04/Screen-Shot-2018-04-20-at-10.37.13-am-1024x852.png)

This tool comes in handy when you have finished implementing your ePL program and you feel it is ready to be broadcast to the XEL network.  
Xeline basically is a wallet software which lets you easily upload your ePL file to the XEL network by just drag-dropping it into the GUI. It takes only a few seconds to have the computation nodes on the XEL network start searching for solutions to your algorithm. Furthermore, this wallet is able to conveniently perform live monitoring of your open tasks and gathers + collects the results that other nodes have found and recorded on the Blockchain.

The installation is straightforward.

[**Windows**](https://docs.elastic.pw/t/xeline_wallet/windows)

[**MacOS**](https://docs.elastic.pw/t/xeline_wallet/macos)

[**Linux**](https://docs.elastic.pw/t/xeline_wallet/linux)

## **Preparing Your ePL File**

We will use our demonstration task \([found here\)](https://xeline.org/programming-in-epl) in this tutorial. Save it to a file called “my\_own\_prime\_demo.epl”. While this demo is already integrated in the Xeline wallet and can be run right away, we want to create this demo project from scratch here – for learning purposes. At this moment, your ePL file contains just the program logic. However, to submit it to the Blockchain you have to configure a few parameters which we can “metadata. Those parameters tell Xeline how much you are willing to spend for that job, how long it is meant to be running, how many solutions you are interested in, how many iterations your job is meant to run, and so on. We have not yet covered the iteration part, we save that for later. Metadata is added to your ePL file at the top. So go ahead, an add those lines to the top of your ePL program:

{% code-tabs %}
{% code-tabs-item title="\#metadata" %}
```c
// metadata(title:My personal PRIME demo)
// metadata(pow_limit:1000)
// metadata(pow_price:0.02)
// metadata(bounty_limit:1)
// metadata(bounty_price:5)
// metadata(iterations:1)
// metadata(timeout:250)
// metadata(callback:my_own_prime_demo_callback.js)
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Lets break this up and take a deeper look at what these lines actually do:

{% code-tabs %}
{% code-tabs-item title="\#info" %}
```c
// metadata(title:My personal PRIME demo)
```
{% endcode-tabs-item %}
{% endcode-tabs %}

This line gives your job a description. Try to keep it as short as possible. This title is just used to help you organise tasks inside the Xeline wallet and it won’t be transmitted to the Blockchain.

{% code-tabs %}
{% code-tabs-item title="\#info" %}
```c
// metadata(pow_limit:1000)
// metadata(pow_price:0.0001)
```
{% endcode-tabs-item %}
{% endcode-tabs %}

These two lines describe how many proof-of-work rewards you want to give out before your job times out and closes automatically. Remember: these are continuous small rewards workers keep getting as a targeted frequency of 10 proof-of-work / second \(for the all tasks in the network together\). So in our case, we want to close our job if we have paid 1000 proof-of-work rewards for 0.0001 XEL each and the network has not yet found a solution to our problem.

{% code-tabs %}
{% code-tabs-item title="\#info" %}
```c
// metadata(bounty_limit:1)
// metadata(bounty_price:5)
```
{% endcode-tabs-item %}
{% endcode-tabs %}

These two lines describe how many solutions you want to your problem. In our case, we are looking for just one prime number so we set this value to 1. Also, we are willing to pay a “bounty price” of 5 XEL for the first submitted solution to our problem. If multiple solutions are submitted inside one block, only the one appearing first in the block transaction list will count. This can happen for the very simple reason that the work closing and timeout events are triggered after the block has been processed. So when your job receives a solution in block 1000, it will be closed in block 1001. However, since we can never be sure which unconfirmed transactions will make it into the next block, we cannot close the job after the first solution is put into the unconfirmed transaction cache at block height 1000. This, however, should be not of your concern. This just affects “workers” who have submitted a bounty solution and wonder why they have not been rewarded.

{% code-tabs %}
{% code-tabs-item title="\#info" %}
```c
// metadata(iterations:1)
```
{% endcode-tabs-item %}
{% endcode-tabs %}

This line tells Xeline how many iterations you want your program to run. The concept of iterations will be explained in one of the next blog posts: we leave it at 1 for now, which basically means that your program ends immediately after \#bounty\_limit solutions have been found.

{% code-tabs %}
{% code-tabs-item title="\#info" %}
```c
// metadata(timeout:250)
```
{% endcode-tabs-item %}
{% endcode-tabs %}

This line tells Xeline after how many blocks you want to end your task regardless of how many proof-of-work or bounty solutions have been found. This is useful when you, for example, create tasks with time critical results. In this example, we just set this value to a random 250 which means that the job will end after 250 block from the block it gets included into.

{% code-tabs %}
{% code-tabs-item title="\#info" %}
```c
// metadata(callback:my_own_prime_demo_callback.js)
```
{% endcode-tabs-item %}
{% endcode-tabs %}

This line is probably the most important one since it will help you to automatically analyze and post process the results the worker nodes find. Remember, as you have seen in the ePL programming guide, solutions are determined by 12 pseudorandom integers stored in the internal `uint m[12];` array. Depending on how complex the way you derive your solution candidates from is, it may be close to impossible to extract your actual solution from just looking at this array. This is the job of our so-called callback.

But specifying the callback in the metadata is not enough, we actually need to create that file in the correct location. The directory where callback scripts should be placed into varies by operating system:

**Windows:**

{% code-tabs %}
{% code-tabs-item title="\#path" %}
```javascript
C:\Users\YourUserName\AppData\Local\Xeline\callbacks
```
{% endcode-tabs-item %}
{% endcode-tabs %}

**MacOS:**

{% code-tabs %}
{% code-tabs-item title="\#path" %}
```javascript
~/Library/Application Support/Xeline/callbacks
```
{% endcode-tabs-item %}
{% endcode-tabs %}

**Linux:**

{% code-tabs %}
{% code-tabs-item title="\#dir" %}
```javascript
~/.config/Xeline/callbacks
```
{% endcode-tabs-item %}
{% endcode-tabs %}

So, if you are on a macOS system you have to create the following file for this demo to run:

{% code-tabs %}
{% code-tabs-item title="\#file" %}
```javascript
~/Library/Application Support/Xeline/callbacks/my_own_prime_demo_callback.js
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Callbacks are written in NodeJS and are only executed on your local computer. As said before, they are meant to nicely post process your solution candidate for display. Practically, the Xeline wallet will run this file once a solution has been submitted to the Blockchain and display the console output in your task overview. Of course, your callback can do all sorts of other stuff like, for example, submit your result over the network or feed it into another application. For now, just put this line into the file:

{% code-tabs %}
{% code-tabs-item title="\#add" %}
```bash
console.log("Yeah. The blockchain just reported this prime: " + (bounties[0][0]>>>0));
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Within your callback script, you can access a two-dimensional array called `bounties[][]`. The first dimension holds all solutions that were submitted, and the second dimension holds the 12 `m[]`values that led to this solution. Since we are only looking for one solution only, our bounty array will have just one entry containing twelve unsigned integers:

{% code-tabs %}
{% code-tabs-item title="\#info" %}
```c
var bounties = [ [m[0],m[1],m[2],...m[11]] ];
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Since our prime number candidate is just in `m[0]` \(if you do not understand this, read the ePL programming guide again\) it is enough for us to just print out `bounties[0][0]`, i.e., the first m value in the first \(and only\) solution.

There is a second, one-dimensional array that you can access, the `storages[]` array which contains the latest version of the storage integers. Since we have not yet used the concept of iterations and storages, this array will be empty and should not be accessed in this demo.

## **Submitting Your Task to the Blockchain**

Now, it’s time to submit your task to the Blockchain. To do so, click on “new task” in the lower part of the left hand side in order to go to the “New Task” screen:

![](https://xeline.org/wp-content/uploads/2018/04/Screen-Shot-2018-04-20-at-12.23.31-pm-1024x852.png)

Now, simply drag your “my\_own\_prime\_demo.epl” file onto the drag-drop field:

![](https://xeline.org/wp-content/uploads/2018/04/Screen-Shot-2018-04-20-at-12.27.20-pm-1024x815.png)

You will see a confirmation screen where you can once again verify that all the metadata you have configured earlier has been picket up correctly. Also, this step will inform you in case you have not put your callback script in the proper location. By clicking the “Broadcast” button, you can actually submit your task to the Blockchain. You will see this confirmation message, showing the transaction ID and advise you to switch over to your task overview:

![](https://xeline.org/wp-content/uploads/2018/04/Screen-Shot-2018-04-20-at-12.29.20-pm-1024x815.png)

Click on “work list overview” or alternatively on “xx tasks” in the left sidebar in order to switch to the task overview:

![](https://xeline.org/wp-content/uploads/2018/04/Screen-Shot-2018-04-20-at-12.31.35-pm-1024x815.png)

It might happen, that your task does not appear immediately because it needs at least one confirmation on the Blockchain. Just hang on for a minute, it should appear eventually. You will see your task which comes with some basic statistics such as the amount of proof-of-work submissions received so far, the number of bounties \(or solutions\) that have been found so far, the iteration this job is in and the remaining blocks until the job times out. Additionally, for open tasks, you see a “Cancel” button which allow you to stop that job at any time. Below the task statistics you see a message saying, that a callback will be executed the moment the job is finished: this is where the results of your task will appear.

And this is how it looks like after your job has finished and your callback has been executed:

![](https://xeline.org/wp-content/uploads/2018/04/Screen-Shot-2018-04-20-at-12.36.09-pm-1024x815.png)

Congratulations! You have successfully created your first job in ePL, submitted it to the Blockchain, received a result that has been found by a “miner” and automatically analyzed the result within your callback. You are ready to move on and learn about the concepts of iterations and storage.

{% page-ref page="advanced\_tactics.md" %}

>

