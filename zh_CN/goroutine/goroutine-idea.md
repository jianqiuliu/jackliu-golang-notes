# goroutine 个人的idea思考小结

###  Golang不使用OS层process而使用语言层面（Goroutine）处理 并发 & 并行 Task任务方案(针对业务来说)的个人思考和实践思路随想 ---Jack Liu 秋

1.使用OS层面进程管理，虽然成本低廉快捷，但对CPU的性能开销比较大，Golang通过Goroutine的引入，构建一种SandBox沙箱容器式的方案，可以将并发处理任务放在语言层面内部，“隔离“在系统层面之上，构建Goroutine池的同时，也能保证在性能可靠的前提下，安全性也增强。   
目前大规模分布式系统的整体方向，大部分也都是建立在OS系统层之上(而非系统层面)以达到可控的标准控制，将OS系统级内核CPU的开销降到最低保证OS层流畅运行，这也让Linux为代表的服务器OS系统更“专注”做Base底层基础性的业务支撑。

2.系统层面上，抛开编程语言层面不谈，服务端越来越趋于Service服务化和分布式、集群化，以此应对越来越复杂的业务。现有编程语言历史遗留和生态环境等因素处理的成本较高，针对多核CPU使用率也不高，性能问题凸显。  
Golang在服务器端的优势在于，非常低成本将开发人员从以前的单进程类编程语言中解放，提供最低成本快速转变为并行编程的思维模式。
Goroutine并发执行的模式，不放在系统进程处理，好处：  
（1）.安全隔离型设计，限制进程中Task Process处理的边界，在大规模集群服务器中使用相对统一的标准处理方式，最大限度规避OS层面的差异带来的问题；    
（2）.降低OS进程的开销，不因golang的执行导致拖累系统CPU资源；  
（3）.并发Task任务行为和状态可控，内存占用开销小，容量自由扩展；  
（4）.轻量级在协程处理时可靠性高；  
（5）.使用这种机制，可以较低成本构建大型和可伸缩计算和批处理Task任务的应用和程序，一开始Golang的定位就是系统级编程语言，所以二进制的运行性能不会差，现阶段的语言性能之争毫无意义。   

目前业内针对业务处理的大型系统应用的常态应该至少包含两点：  
1.支持最小成本组织大规模数据和计算处理；  
2.Task任务的行为和状态能够可靠、低成本可控。  

云计算追求对服务端在安全可控的前提下软硬件资源的最低成本配置和最佳的资源调度，做的所有分布式、自由伸缩、集群的重要原因也是源为此，Goroutines在这方面大有可为。  

官方一句话说得比较直白和代表性：  
Do not communicate by sharing memory; instead, share memory by communicating.  
不要通过共享内存进行通信，而是通过通信共享内存。

明确并发和并行的两个概念：
并发不是并行：并发是由切换时间来实现“同时”运行，并行是多核多线程 
goroutine 通过通信来共享内存，而不是共享内存来通信。这样就可以较为充分利用多核CPU和内存资源的同时，又相对比较可靠，"协程"也是类似种"管道"的思维模式，在这里，通信显得比较重要，这些Golang已经做了底层化实现，对开发者来说比较简便一些，大部分精力放在管理好这些阀门出入口即可。
Linux的管道是非常优秀的设计。

这个应该不是说以前的方案或其他语言处理思路是错误、不佳或有偏差的，历史上很多方案往往受制于硬件的运算性能综合因素考虑，是当时权衡下来的最好的方案，比如硬件成本太高等，现在随着软硬件的快速发展和成本低廉有这个条件来做这个事情了。终归是有当时基于现实情况的各种因素考量。 
无论性能再怎么快，必须把可靠性放在重要位置，一个相对不可靠的方案，程序运行速度再快将毫无意义，我想这是Golang从软件工程化考虑的重要考量吧。  

Golang设计哲学和Unix应该是一致的：大道至简，“简”是对大规模工程化系统开发中最好的思考范畴，虽万变仍不离其宗。 

并发&并行的编程理念对开发人员来说是未来编程思维的常态，事物发展的规律。  

至少在公司产品和项目开发中，Golang至少是未来主力的语言，因为随着数据的不断增长，必须要一种从性能上，可靠性上和开发上相对最合适的技术选型，Golang是很符合这一点的，Golang不只是一个简单的编程语言这么简单。  
C系的开发语言经久不衰很重要的原因就是追求用最简单的方式解决现实问题，Golang是未来考虑的主力开发语言。  
### 个人实践思路示意：
 ![image](https://github.com/iotd/jackliu-golang-notes/blob/master/zh_CN/done-mode.jpg)

                                                                  --------- Jack Liu 秋    Date：2017-05-30
