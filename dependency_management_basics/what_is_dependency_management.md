# 什么是依赖管理?

粗略的讲, 依赖管理由两部分组成. 首先, Gradle需要了解你的项目需要构建或运行的东西,一遍找到他们. 我们称这些传入的文件为项目的*dependencies(依赖项)*. 其次, Gradle 需要构建并上传你的项目产生的东西. 我们称这写传出的项目文件为*publications(发布项)*.让我们来看看这两条的详细信息：

大多数项目都不是完全独立的. 它们需要其他项目进行编译或测试等等. 举个例子,为了在项目中使用Hibernate,我要在我编译的时候在我的`classpath`中包括一些Hibernate的jar. 要运行测试的时候,我需要在`test classpath`中包含一些额外的jar,比如特定的JDBC驱动或者`Ehcache jars`.

这些传入的文件构成上述的项目的依赖. Gradle允许你告诉它你项目的依赖关系,以便找到这些依赖关系,并在你的构建中维护这些依赖关系.依赖关系可能需要从远程的Maven或者Ivy仓库中下载,也可能是在本地文件系统中,或者是通过多项目构建另一个构建. 我们称这个过程为*dependency resolution(依赖解析)*.

注意这一特性提供了超过Ant的一个重要特性.使用Ant,你只有指定jar的绝对路径或相对路径才能读取jar.使用Gradle,你只需要申明依赖的名称,其他层面决定这在哪里获取这些依赖关系.你可以为Ant添加Apache的Ivy或得类似能力,但是Gradle做的更好.

通常,一个项目的本身会具有依赖性.举个例子,运行Hibernate的核心需要其他几个类库在classpath中.因此,Gradle在为你的项目运行测试的时候,它会找到这些依赖关系,并使其可用.我们称之为*transitive dependencies(依赖传递)*.

大部分项目的主要目的是要建立一些文件,在项目之外使用.比如,你的项目产生一个Java库,你需要构建一个jar,可能是一个jar和一些文档,并将它们发布在某处.

这写传出文件构成了项目的发布物. Gradle当然会为你照顾这个重要的工作. 你声明项目的出版物,Gradle会构建并发布在某处. 究竟什么是"出版"取决于你想做什么.可能你希望将文件复制到本地目录,或者将他们上传到一个远程Maven或者Ivy库.或者你可以使用这些文件在多项目构建中另外的项目中.我们称这个过程为*publication(发布)*


