# About

ePL is a programming language which was specifically designed for coding algorithms to be executed on the XEL computation node network. 

Its syntax is very similar to the C programming languages. However, since nodes on the XEL network download and execute code from potentially dangerous sources, a few adaptations were necessary to ensure that code written in ePL can cause no harm to the system it is executed on. 

Furthermore, since task distribution and verification is done in a decentralized fashion \(all nodes which meet a minimum system requirement in terms or memory and CPU power must be able to verify the algorithms’ results in a similar amount of time\) it is designed to run in a resource-limited VM. Furthermore, ePL has a slightly modified memory management \(and instruction set\) which ensures that every node can assess how much memory the program will consume and when it will terminate prior to execution. This avoids unpredictable behavior such as out of memory errors and the halting problem.

![ElasticPL \(ePL\) visualized ](../../.gitbook/assets/undefined%20%287%29.png)

{% page-ref page="programming\_tasks.md" %}

>

