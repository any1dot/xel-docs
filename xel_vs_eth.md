# XEL VS ETHEREUM

## Two Different Systems With Two Different Use-cases

Many people mistake Ethereum for a large super computer suitable for distributed computation tasks. However, this is not the type of problem that Ethereum is meant to solve. Ethereum, to emphasize once again, does not try to exploit the number of nodes in the network for solving certain computations faster.

![](http://elastic.sc/docs/wp-content/uploads/2018/03/blk-2.png)

## **Figure 1**

Depicts how computations are performed on the Ethereum network. Imagine you have a smart contract in source code form that has been uploaded to the Blockchain; this smart contract is depicted by the upper white rectangle while each node in the Ethereum network is represented by one square in the lower rectangle. The crucial part about understanding the difference between Ethereum and XEL now is to understand that the smart contract’s source code is executed – in its entirety – on every single node in the network. The purpose to do so is to form a strong consensus about the outcome of the result of the execution. Imagine the smart contract is programmed to release a certain amount of Ether, the underlying currency of Ethereum, at a certain Blockchain height to a specific ETH address: when all nodes execute the same code, they can form a consensus about their view on the current state, and – in this case – on the balance of the aforementioned ETH address.

While this type of distributed consensus is very powerful to ensure integrity of code execution across all nodes in the network, it is unsuitable to speed up the execution of complex computation tasks. That is, when there are 1000 equal full-nodes participating in the Ehereum network, then the entire smart contract is executed exactly 1000 times \(and not 1000 times faster\). This is similar to a more complex variant of the Bitcoin transaction verification method where every node must execute the same verification algorithm \(which also is just source code, it is just hard-wired into the Bitcoin client\) so that the network as a whole can jointly agree upon whether a transaction was valid and executed or not.

The computation model in XEL is quite different from what we find in Ethereum. Instead of ensuring that every node executes the same code in the same way, the goal is to use the joint computational power of a group of online nodes in order to solve a computation task as fast as possible. 

## **Figure 2** 

Depicts the computation model as it is used in XEL. Again – depicted by the upper white rectangle – we start with a problem statement. This will mostly be an algorithm which is meant to solve some arbitrary hard computation task. Then – depicted by the fine grid at the bottom – there is a task splitting strategy: this is a command and conquer strategy, which splits the large problem statement into many small sub-problems. To give you a short example: imagine you have a large unsorted list of numbers and the problem now is to find a particular one in it. The naive approach would be to scan through the entire list element by element and compare it to the number we are looking for. Applying the idea of command and conquer to this problem would result in splitting the huge list into a very large amount of very small lists. These sub-lists then can be searched for the desired number independently – if you now have many nodes, each one working on one of these sub-lists – you can solve the problem a lot quicker. Same happens in XEL: problems are divided into sub-problems and \(looking at it from a very high level – a more detailed explanation can be found in the technical details section\) “directed” to individual nodes. The main difference is that every node on the XEL network works on a different portion of the greater problem. The result then can be formed by the combination of one or more results to the individual sub-problems. The more nodes work on these sub-problems, the quicker they come to a solution.

{% page-ref page="arbitrary.md" %}

>

