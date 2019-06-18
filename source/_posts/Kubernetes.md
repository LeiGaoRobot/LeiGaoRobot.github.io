---
title: Kubernetes
date: 2019-05-15 09:17:59
categories: 
- [Container-Orchestration]
- [Kubernetes]
tags:
- container
- microservice
- cloud platform
---

# What is Containerized?

操作系统层虚拟化（英语：Operating system–level virtualization），亦称容器化（英语：Containerization），是一种虚拟化技术，这种技术将操作系统内核虚拟化，可以允许用户空间软件实例（instances）被分割成几个独立的单元，在内核中运行，而不是只有一个单一实例运行。

这个软件实例，也被称为是一个 containers(Solaris, Docker), Zones(Solaris), virtual private servers(OpenVZ), partitions , virutial environments(VEs), virtual kernel(DragonFly BSD) 或是 jails(FreeBSD jail或chroot jail) 。从运行在其中的程序的角度来看，它可能看起来像真正的计算机。在普通操作系统上运行的计算机程序可以看到该计算机的所有资源（连接的设备，文件和文件夹，网络共享，CPU功率，可量化的硬件能力）。但是，在容器内运行的程序只能看到容器的内容和分配给容器的设备。

操作系统层虚拟化之后，可以实现软件的即时迁移（Live migration），使一个软件容器中的实例，即时移动到另一个操作系统下，再重新运行起来。但是在这种技术下，软件即时迁移，只能在同样的操作系统下进行。

在类Unix操作系统中，这个技术最早起源于标准的chroot机制，再进一步演化而成。除了将软件独立化的机制之外，内核通常也提供资源管理功能，使得单一软件容器在运作时，对于其他软件容器的造成的交互影响最小化。

相对于传统的虚拟化（Virtualization），容器化的优势在于占用服务器空间少，通常几秒内即可引导。同时容器的弹性可以在资源需求增加时瞬时复制增容，在资源需求减小时释放空间以供其他用户使用。由于在同一台服务器上的容器实例共享同一个系统内核，因此在运行上不会存在实例与主机操作系统争夺RAM的问题发生，从而能够保证实例的性能。

术语“容器”虽然最普遍地指代OS级虚拟化系统，但有时模糊地用于指代与主机OS不同程度地操作的更全面的虚拟机环境，例如Microsoft的 “Hyper-V容器”。

## Operation

在个人计算机的普通操作系统上，计算机程序可以看到（即使它可能无法访问）所有系统的资源。他们包括：

+ 可以采用的硬件功能，例如CPU和网络连接
+ 可以读取或写入的数据，例如文件，文件夹和网络共享
+ 它可以与之相互连接的外围设备，例如网络摄像头，打印机，扫描仪或传真机
+ 操作系统可能能够基于哪个程序在其运行的上下文中请求它们和用户帐户来允许或拒绝对这些资源的访问。操作系统还可以隐藏这些资源，以便当计算机程序枚举它们时，它们不会出现在枚举结果中。然而，从编程的角度来看，计算机程序已与这些资源交互，并且操作系统已经管理了交互行为。

通过操作系统虚拟化或容器化，可以在容器内运行程序，只分配这些资源的一部分。一个程序希望看到整个计算机，一旦在容器内运行，只能看到分配的资源并认为它们是可用的全部。可以在每个操作系统上创建几个容器，为每个容器分配计算机资源的子集。每个容器可以包含任意数量的计算机程序。这些程序可以同时或分开运行，甚至可以相互交互。

容器化与应用程序虚拟化有相似之处：在后者中，只有一个计算机程序放在隔离的容器中，隔离仅适用于文件系统。

# What is a Container?

一个容器（Linux容器）的核心是主机（计算机）资源的 allocation， portioning 和 assignment，例如 CPU Shares ，网络 I/O ，带宽， 块 I/O 和 内存（RAM），以便内核级别构造可以监控，隔离或“包含”这些受保护的资源，以便特定的运行服务（进程）和命名空间可以单独使用它们而不会干扰系统的其余部分。这些进程可以是基于Linux镜像的轻量级Linux主机，多个Web服务器和应用程序，单个子系统（如数据库后端），也可以是单个进程，例如 echo "Hello"，几乎没有开销。

通常称为 “OS-level virtualization” 或 “OS Vitual Environments” 的 容器 与 虚拟机管理程序级 的 虚拟化 不同。主要区别在于容器模型消除了通常在VM中运行工作负载所需的虚拟机管理程序层，冗余OS内核，二进制文件和库。

# What is Kubernetes?

Kubernetes（常简称为K8s）是用于自动部署、扩展和管理容器化（containerized）应用程序的开源系统，是一个跨主机集群的开源的容器调度平台，它可以自动化应用容器的部署、扩展和操作,提供以容器为中心的基础架构。该系统由Google设计并捐赠给Cloud Native Computing Foundation（今属Linux基金会）来使用。

它旨在提供“跨主机集群的自动部署、扩展以及运行应用程序容器的平台”。它支持一系列容器工具, 包括Docker等。CNCF于2017年宣布首批Kubernetes认证服务提供商（KCSPs），包含IBM、华为、MIRANTIS、inwinSTACK迎栈科技等服务商。

## Kubernetes and Docker

Kubernetes不会取代Docker，但会增加它。但是，Kubernetes 确实取代了Docker中出现的一些更高级别的技术。

其中一种技术是Docker Swarm，一个与Docker捆绑在一起的编排器。仍然可以使用Docker Swarm而不是Kubernetes，但Docker Inc.已经选择让Kubernetes成为Docker社区和Docker Enterprise版本的一部分。

并不是说Kubernetes是Docker Swarm的直接替代品。Kubernetes比Swarm复杂得多，需要更多的工作才能部署。但同样，这项工作旨在从长远来看提供巨大的回报 - 一个更易于管理，更具弹性的应用程序基础架构。对于开发工作和较小的容器集群，Docker Swarm提供了一个更简单的选择。 

## Kubernetes and Mesos

作为Kubernetes的竞争对手，你可能听说过的另一个项目是Mesos。Mesos是一个Apache项目，最初来自Twitter的开发人员; 它实际上被视为Google Borg项目的答案。

事实上，Mesos确实提供了容器编排服务，但它的雄心远不止于此：它的目标是成为一种可以协调容器化和非容器化组件的云操作系统。为此，许多不同的平台可以在Mesos中运行 - 包括Kubernetes本身。

## Why use containers?

![gcheap](/img/kubernetes/why_containers.svg)

传统 部署应用程序的方式，一般是使用操作系统自带的包管理器在主机上安装应用依赖，之后再安装应用程序。这无疑将应用程序的可执行文件、应用的配置、应用依赖库和应用的生命周期与宿主机操作系统进行了紧耦合。在此情境下，可以通过构建不可改变的虚拟机镜像版本，通过镜像版本实现可预测的发布和回滚，但是虚拟机实在是太重量级了，且镜像体积太庞大，便捷性差。

新方式 是基于操作系统级虚拟化而不是硬件级虚拟化方法来部署容器。容器之间彼此隔离并与主机隔离：它们具有自己的文件系统，不能看到彼此的进程，并且它们所使用的计算资源是可以被限制的。它们比虚拟机更容易构建，并且因为它们与底层基础架构和主机文件系统隔离，所以它们可以跨云和操作系统快速分发。

由于容器体积小且启动快，因此可以在每个容器镜像中打包一个应用程序。这种一对一的应用镜像关系拥有很多好处。使用容器，不需要与外部的基础架构环境绑定, 因为每一个应用程序都不需要外部依赖，更不需要与外部的基础架构环境依赖。完美解决了从开发到生产环境的一致性问题。

容器同样比虚拟机更加透明，这有助于监测和管理。尤其是容器进程的生命周期由基础设施管理，而不是由容器内的进程对外隐藏时更是如此。最后，每个应用程序用容器封装，管理容器部署就等同于管理应用程序部署。

容器优点摘要:

+ 敏捷的应用程序创建和部署: 与虚拟机镜像相比，容器镜像更容易创建，提升了硬件的使用效率。
+ 持续开发、集成和部署: 提供可靠与频繁的容器镜像构建和部署，可以很方便及快速的回滚 (由于镜像不可变性).
+ 关注开发与运维的分离: 在构建/发布时创建应用程序容器镜像，从而将应用程序与基础架构分离。
+ 开发、测试和生产环境的一致性: 在笔记本电脑上运行与云中一样。
+ 云和操作系统的可移植性: 可运行在 Ubuntu, RHEL, CoreOS, 内部部署, Google 容器引擎和其他任何地方。
+ 以应用为中心的管理: 提升了操作系统的抽象级别，以便在使用逻辑资源的操作系统上运行应用程序。
+ 松耦合、分布式、弹性伸缩 微服务: 应用程序被分成更小，更独立的部分，可以动态部署和管理 - 而不是巨型单体应用运行在专用的大型机上。
+ 资源隔离: 通过对应用进行资源隔离，可以很容易的预测应用程序性能。
+ 资源利用: 高效率和高密度。

## Kubernetes Feature

最基础的，Kubernetes 可以在物理或虚拟机集群上调度和运行应用程序容器。然而，Kubernetes 还允许开发人员从物理和虚拟机’脱离’，从以主机为中心的基础架构转移到以容器为中心的基础架构，这样可以提供容器固有的全部优点和益处。Kubernetes 提供了基础设施来构建一个真正以容器为中心的开发环境。

Kubernetes 满足了生产中运行应用程序的许多常见的需求，例如：

+ Pod 提供复合应用并保留一个应用一个容器的容器模型
+ 挂载外部存储
+ Secret管理
+ 应用健康检查
+ 副本应用实例
+ 横向自动扩缩容
+ 服务发现
+ 负载均衡
+ 滚动更新
+ 资源监测
+ 日志采集和存储
+ 支持自检和调试
+ 认证和鉴权

这提供了平台即服务 (PaaS) 的简单性以及基础架构即服务 (IaaS) 的灵活性，并促进跨基础设施供应商的可移植性。

有关详细信息，请参阅[kubernetes docs](https://kubernetes.io/zh/docs/concepts/overview/what-is-kubernetes/)

Kubernetes 提供了很多的功能，总会有新的场景受益于新特性。它可以简化应用程序的工作流，加快开发速度。被大家认可的应用编排通常需要有较强的自动化能力。这就是为什么 Kubernetes 被设计作为构建组件和工具的生态系统平台，以便更轻松地部署、扩展和管理应用程序。

Kubernetes 不是一个传统意义上，包罗万象的 PaaS (平台即服务) 系统。

+ Kubernetes 不限制支持的应用程序类型。 它不插手应用程序框架 (例如 Wildfly), 不限制支持的语言运行时 (例如 Java, Python, Ruby)，只迎合符合 12种因素的应用程序，也不区分”应用程序”与”服务”。Kubernetes 旨在支持极其多样化的工作负载，包括无状态、有状态和数据处理工作负载。如果应用可以在容器中运行，它就可以在 Kubernetes 上运行。
+ Kubernetes 不提供作为内置服务的中间件 (例如 消息中间件)、数据处理框架 (例如 Spark)、数据库 (例如 mysql)或集群存储系统 (例如 Ceph)。这些应用可以运行在 Kubernetes 上。
+ Kubernetes 没有提供点击即部署的服务市场
+ Kubernetes 从源代码到镜像都是非垄断的。 它不部署源代码且不构建您的应用程序。 持续集成 (CI) 工作流是一个不同用户和项目都有自己需求和偏好的领域。 所以支持在 Kubernetes 分层的 CI 工作流，但不指定它应该如何工作。
+ Kubernetes 允许用户选择其他的日志记录，监控和告警系统 (虽然我们提供一些集成作为概念验证)
+ Kubernetes 不提供或授权一个全面的应用程序配置语言/系统 (例如 jsonnet).
+ Kubernetes 不提供也不采用任何全面机器配置、保养、管理或自我修复系统

另一方面，许多 PaaS 系统运行 在 Kubernetes 上面，例如 Openshift, Deis, and Eldarion。 您也可以自定义您自己的 PaaS, 与您选择的 CI 系统集成，或与 Kubernetes 一起使用: 将您的容器镜像部署到 Kubernetes。

由于 Kubernetes 在应用级别而不仅仅在硬件级别上运行，因此它提供 PaaS 产品通用的一些功能，例如部署、扩展、负载均衡、日志记录、监控等。但是，Kubernetes 不是单一的，默认解决方案是可选和可插拔的。

此处，Kubernetes 不仅仅是一个 “编排系统”；它消除了编排的需要。 “编排”技术定义的是工作流的执行: 从 A 到 B，然后到 C。相反，Kubernetes 是包括一套独立、可组合的控制过程，通过声明式语法使其连续地朝着期望状态驱动当前状态。 不需要告诉它具体从 A 到 C 的过程，只要告诉到 C 的状态即可。 也不需要集中控制；该方法更类似于”编舞”。这使得系统更容易使用并且更强大、更可靠、更具弹性和可扩展性。

# How Kubernetes works

Kubernetes的架构利用了各种概念和抽象。其中一些是现有的，熟悉的概念的变体，但其他一些是Kubernetes特有的。

## Kubnernetes clusters

最高级别的Kubernetes抽象即集群，指的是运行Kubernetes（本身是集群应用程序）的计算机组以及由它管理的容器。Kubernetes集群必须具有主服务器，该系统可以命令和控制集群中的所有其他Kubernetes计算机。一个高可用性集群Kubernetes复制到多台机器主人的设施。但是，一次只有一个主服务器运行作业调度程序和控制器管理器。

## Kubernetes node and pods

每个群集都包含 Kubernetes 节点。节点可能是物理机器或VM。同样，这个想法是抽象的：无论运行什么应用程序，Kubernetes都会处理该基板上的部署。Kubernetes甚至可以确保某些容器仅在VM上运行或仅在裸机上运行。

节点运行 pod ，这是可以创建或管理的最基本的Kubernetes对象。每个pod代表Kubernetes中的应用程序或运行进程的单个实例，由一个或多个容器组成。Kubernetes作为一个组启动，停止和复制pod中的所有容器。Pod将用户的注意力集中在应用程序上，而不是容器本身上。有关如何配置Kubernetes的详细信息，从pod的状态开始，保存在Etcd（一个分布式键值存储）中。

根据需要在节点上创建和销毁Pod，以符合用户在pod定义中指定的所需状态。Kubernetes提供了一个称为控制器的抽象概念，用于处理pod的组织管理，Spun up，rolled out 和 spun down。控制器有几种不同的风格，具体取决于所管理的应用程序的类型。例如，最近引入的“StatefulSet”控制器用于处理需要持久状态的应用程序。另一种控制器，即部署，用于向上或向下扩展应用程序，将应用程序更新为新版本，或者在出现问题时将应用程序回滚到已知良好版本。

## [Kubernetes Service](https://kubernetes.io/docs/concepts/services-networking/service/)

因为 pods 根据需要会有出生和死亡，我们需要一个不同的抽象来处理应用程序生命周期。应用程序应该是一个持久化实体，即使运行构成应用程序的容器的pod本身不是持久的。为此，Kubernetes提供了一种称为服务的抽象。

Kubernetes中的服务描述了如何通过网络访问给定的pod组（或其他Kubernetes对象）。正如Kubernetes文档所说，构成应用程序后端的pod可能会发生变化，但前端不需要知道或跟踪它。服务使这样成为可能。

Kubernetes的调度程序将工作负载分配给节点，以便在资源之间实现平衡，从而使部署满足应用程序定义的要求。controller manager 确保系统应用程序、工作负载等的状态匹配Etcd配置设置中定义的所需状态。

重要的是要记住，容器使用的任何底层机制（如Docker本身）都不会被 Kubernetes 取代。相反，为了保持应用程序大规模运行，Kubernetes为使用这些机制提供了更多的抽象化。

## [Kubernetes Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)

Kubernetes服务被认为是在集群中运行。但是您希望能够从外部世界访问这些服务。Kubernetes有几个组件可以通过不同程度的简化并具有健壮性的来实现这一点，包括NodePort和LoadBalancer，但具有最大灵活性的组件是Ingress。Ingress是一种API，通常通过HTTP管理对集群服务的外部访问。

Ingress确实需要一些配置来正确设置 - 马修帕尔默写了一本关于Kubernetes开发的书，在他的网站上会引导你完成整个过程。[Kubernetes Ingress with Nginx Example](https://matthewpalmer.net/kubernetes-app-developer/articles/kubernetes-ingress-guide-nginx-example.html)

## [Kubernetes Dashboard](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)

一个帮助您掌握所有其他组件的Kubernetes组件是Dashboard，这是一个基于Web的UI，您可以使用它来部署和排除应用程序故障并管理群集资源。默认情况下不安装仪表板，但[添加它](https://dzone.com/articles/how-to-install-the-kubernetes-dashboard)并不是太麻烦。

## Kubernets Advantages

因为Kubernetes引入了新的抽象和概念，并且因为Kubernetes的学习曲线很高，所以询问使用Kubernetes的长期收益是正常的。以下是在Kubernetes中运行应用程序的一些具体方法的简要说明。

## Manages app health, replication, load balancing, and hardware resource allocation

Kubernetes最基本的职责之一就是保持应用程序的正常运行和响应用户的需求。那些变得“不健康”，或者不符合你描述的健康定义的应用程序，可以自动修复。

Kubernetes提供的另一个好处是最大限度地利用硬件资源，包括内存，存储I/O和网络带宽。应用程序可以对其资源使用设置软限制和硬限制。许多使用最少资源的应用程序可以在同一硬件上一起打包;需要延伸的应用程序可以放置在有增长空间的系统上。同样，在集群中推出更新，或者如果更新中断，则可以自动回滚。

## Eases the deployment of preconfigured applications with [Helm](https://helm.sh/) charts

不同版本Linux的软件包管理器和Python的Pip等软件包管理器为用户省去了手动安装和配置应用程序的麻烦。当应用程序具有多个外部依赖项时，这尤其方便。

Helm 本质上是Kubernetes的包管理器。许多流行的软件应用程序必须作为一组相互依赖的容器在Kubernetes中运行。 Helm提供了一个定义机制，a "chart," 描述了如何在Kubernetes中将应用程序或服务作为一组容器运行。

您可以从头开始创建自己的 Helm charts，如果您要构建要在内部部署的自定义应用程序，则可能需要这样做。但是，如果您使用的是具有通用部署模式的流行应用程序，则很有可能有人已经为其创建了 Helm chart 并将其发布到官方 Helm charts 存储库中。另一个寻找官方 Helm charts 的地方是 [Kubeapps.com directory](https://kubeapps.com/)

## Simplifies management of storage, secrets, and other application-related resources

容器意味着不可改变;你放入的任何东西都不应该改变。但是应用程序需要状态，这意味着它们需要一种可靠的方式来处理外部存储卷。容器在应用程序的生命周期中生存，死亡和重生的方式变得更加复杂。

Kubernetes提供抽象化，允许容器和应用程序以与其他资源相同的分离方式处理存储。从 Amazon EBS volumes 到 plain old NFS shares, 可以通过 Kubernetes storage drivers(volumes.Normally) 访问 。通常， volumes 被绑定到特定的 pod ，但称为 "Persisten Volume" 的 volume 子类型可用于需要独立于任何 pod 进行生存的数据。

容器通常需要处理 “secrets”-诸如是API密钥或服务密码一样的凭证，您不希望凭证硬编码到容器中或公开存储在磁盘卷中。虽然可以使用第三方解决方案，例如 Docker secrets 和 HashiCorp Vault ，但Kubernetes有自己的秘密处理机制，尽管它确实需要谨慎配置。例如，**必须将 Etcd 配置为在节点之间而不是纯文本中发送秘密时使用 SSL/TLS 。

## Applications can run in hybrid and muti-cloud environments

云计算的长期梦想之一是能够在任何云中运行任何应用程序，或者在公共或私有云的任何组合中运行。这不仅可以避免供应商锁定，还可以利用特定于各个云的功能。

Kubernetes提供了一组基本类型，统称为 [federation](https://kubernetes.io/docs/concepts/cluster-administration/federation/)，用于使多个集群在多个区域和云中保持同步。例如，给定的应用程序部署可以在多个集群之间保持一致，并且不同的集群可以共享服务发现，以便可以从任何集群访问后端资源。无论您是否跨越多个云环境， federation 还可用于创建高可用性或容错Kubernetes部署。

Federation 对 Kubernetes 来说还是比较新的。并非所有 federation 实例都支持所有API资源，并且可以升级还没有自动测试基础结构。但是这些缺点将在未来版本的Kubernetes中得到解决。

## Usage scenario

Kubernetes有多种形式 - 从开源位到商业支持的分发到公共云服务 - 最好的方法来确定从哪里获得它是用例。

+ 如果您想自己完成这些工作：可以从 [GitHub repository for Kubernetes](https://github.com/kubernetes/kubernetes) 下载源代码和大多数常见平台的预构建二进制文件。
+ 如果您正在使用 Docker Community 或 Docker Enterprise：Docker的最新版本附带Kubernetes作为打包。这显然是容器专家最容易与Kubernetes合作的方式，因为它是通过几乎肯定已经熟悉的产品来实现的。
+ 如果您正在部署或在私有云中部署：私有云选择的任何基础架构都可能都内置了Kubernetes。标准问题，认证，支持的Kubernetes发行版可从许多供应商处获得，包括Canonical，IBM，Mesosphere，Mirantis，Oracle，Pivotal，Red Hat，Suse，VMware等等。
+ 如果您在公共云中部署：三大公共云供应商都提供Kubernetes即服务。 Google Cloud Platform提供Google Kubernetes Engine。 Microsoft Azure提供Azure Kubernetes服务。亚马逊已将Kubernetes添加到其现有的弹性容器服务中。管理型Kubernetes服务也可从IBM，Nutanix，Oracle，Pivotal，Platform9，Rancher Labs，Red Hat，VMware和许多其他供应商处获得。

## Kubernetes Toturials

https://kubernetes.io/docs/tutorials/ -- Kubernetes offical toturials

https://medium.com/quick-code/top-tutorials-to-learn-kubernetes-e9507e76d9a4 -- Top Tutorials To Learn Kubernetes

https://www.infoworld.com/article/3207686/how-to-get-started-with-kubernetes.html -- How to get started with Kubernetes


# 主要参考资源

## [Wikipedia - OS-level virtualisation](https://en.wikipedia.org/wiki/OS-level_virtualisation)

## [kubernetes.io - what is kubernetes](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/)

## [kubernetes.io - Tasks](https://kubernetes.io/docs/tasks/)

## [kubernetes.io - Tutorials](https://kubernetes.io/docs/tutorials/)

## [Kubeapps.com directory](https://kubeapps.com/)

## [helm official webside](https://helm.sh/)

## [infoworld - What is Kubernetes? Container orchestration explained](https://www.infoworld.com/article/3268073/what-is-kubernetes-container-orchestration-explained.html)

## [Linux Containers: Parallels, LXC, OpenVZ, Docker and More](https://aucouranton.com/2014/06/13/linux-containers-parallels-lxc-openvz-docker-and-more/)

## [Kubernetes Ingress with Nginx Example](https://matthewpalmer.net/kubernetes-app-developer/articles/kubernetes-ingress-guide-nginx-example.html)