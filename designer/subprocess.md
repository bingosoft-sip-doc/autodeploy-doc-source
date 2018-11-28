#### 子流程处理多机部署的问题

在多机部署的场景中，几台机器执行的一系列动作都是相同的，这种场景可以借用子流程来做。

![img](..\image\subprocess.png)

例如，一主多从的web负载场景，web节点通过子流程，只需要描述一次tomcat的部署过程即可。子流程的类型设置为`Parallel`表示子流程并行执行。多实例的数量，可以通过参数引用的方式取值，表示多机器的数量。

子流程根据循环调用的数量，会在编号后加上后缀，例如tomcat服务器的编号为tomcat，则实际产生的实例为tomcat01,tomcat02。

如果负载均衡节点，要获取所有tomcat的IP地址，则可以通过`${outputs.tomcat.privateIp}`，得到的将会是一个数组。

子流程内部的引用可以忽略后缀带来的影响，直接以`${outputs.tomcat.privateIp}`表达式，就可以取到当前循环的机器IP地址了。

> 了解更多流程的设计和参数的引用，请参考https://siprs-doc.github.io/designer/modelDesigne.html

> 对于各执行器的能力及其输入输出定义，可以参阅本文档第4节内容，也可以在菜单**高级服务->执行器**中查看。