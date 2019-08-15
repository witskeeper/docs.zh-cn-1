---
title: 设计面向微服务的应用程序
description: 适用于容器化 .NET 应用程序的 .NET 微服务体系结构 | 了解面向微服务的应用程序的优点和缺点，以便可以采取明智的决策。
ms.date: 10/02/2018
ms.openlocfilehash: dfb1619bab68814bd14224e5b50a75d99525a802
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2019
ms.locfileid: "68675964"
---
# <a name="designing-a-microservice-oriented-application"></a>设计面向微服务的应用程序

本部分重点介绍开发假设服务器端企业应用程序。

## <a name="application-specifications"></a>应用程序规范

假设应用程序通过执行业务逻辑、访问数据库，并返回 HTML、JSON 或 XML 响应处理请求。 我们将假定该应用程序必须支持多种客户端，包括运行单页面应用程序W (SPA)、传统 web 应用、移动 web 应用和本机移动应用的桌面浏览器。 应用程序可能还会公开一个 API，供第三方使用。 它还应异步集成其微服务或外部应用程序，因此该方法有助于在发生部分失败时恢复微服务。

应用程序将包括以下类型的组件：

- 演示组件。 该组件负责处理 UI 并使用远程服务。

- 域或业务逻辑。 这是应用程序的域逻辑。

- 数据库访问逻辑。 这包括负责访问数据库（SQL 或 NoSQL）的数据访问组件。

- 应用程序集成逻辑。 这包括主要基于消息代理的消息传递通道。

应用程序需要高可伸缩性，同时允许其垂直的子系统自主横向扩展，因为某些子系统需要比其他子系统更大的可伸缩性。

应用程序必须能在多个基础结构环境（多个公有云和本地）中部署，最好是跨平台，可从 Linux 轻松移动到 Windows（反之亦然）。

## <a name="development-team-context"></a>开发团队上下文

我们还对应用程序的开发过程进行以下假设：

- 不同的开发团队专注于应用程序的不同业务方面。

- 新的团队成员必须快速提高工作效率，且应用程序必须易于理解和修改。

- 应用程序将具有长期发展和不断变化的业务规则。

- 你需要良好的长期可维护性，这意味着在未来实现新更改时具有灵活性，同时能够更新多个子系统，且尽可能减少对其他子系统的影响。

- 你希望执行应用程序的持续集成和持续部署。

- 你希望利用新兴技术（框架、编程语言等），同时发展应用程序。 你不想在转换为新技术时，对应用程序进行完整迁移，因为这样做会产生高额费用，且影响应用程序的可预测性和稳定性。

## <a name="choosing-an-architecture"></a>选择体系结构

应用程序部署体系结构应该是什么？ 根据应用程序的规格以及开发上下文，应用程序的构建应采用以下方式：将其分解为独立的子系统（采用协作的微服务和容器的形式），其中微服务是容器。

在此方法中，每个服务（容器）实现一组紧密结合且关联的功能。 例如，应用程序可能包含目录服务，订购服务、购物篮服务、用户个人资料服务等服务。

微服务不仅使用 HTTP (REST) 等协议通信，而且尽可能进行异步通信（如使用 AMQP），尤其是传播集成事件更新时。

微服务作为相互独立的容器开发和部署。 这意味着开发团队在开发和部署特定微服务时，不会影响其他子系统。

每个微服务都有自己的数据库，从而能够从其他微服务中完全分离。 如有必要，可使用应用程序级集成事件（通过逻辑事件总线）实现不同微服务中的数据库间的一致性，正如命令查询职责分离 (CQRS) 中的处理一样。 由此，业务约束必须接受多个微服务和相关数据库之间的最终一致性。

### <a name="eshoponcontainers-a-reference-application-for-net-core-and-microservices-deployed-using-containers"></a>eShopOnContainers：使用容器部署的 .NET Core 和微服务的参考应用程序

这样一来，你可专注于体系结构和技术，而无需考虑自己可能不知道的假设业务领域，我们已经选择了一个知名的业务领域，即简化的电子商务 (e-shop) 应用程序，它可以提供产品目录、处理客户订单、验证库存并执行其他业务功能。 此基于容器的应用程序源代码可通过 [eShopOnContainers](https://aka.ms/MicroservicesArchitecture) GitHub 存储库获取。

该应用程序包含多个子系统，包括多个应用商店 UI 前端（一个 Web 应用程序和本机移动应用），以及用于所有所需服务器端操作的后端微服务和容器（将多个 API 网关作为合并入口点）。 图 6-1 显示了参考应用程序的体系结构。

![移动和 SPA 客户端与单一 API 网关终结点进行通信，后者随后与微服务进行通信。 传统 Web 客户端与 MVC 微服务进行通信，后者与微服务进行通信](./media/image1.png)

**图 6-1**. 开发环境的 eShopOnContainers 参考应用程序体系结构

**宿主环境**。 在图 6-1 中，你会看到一个 Docker 主机中部署的多个容器。 使用 docker-compose up 命令部署到单个 Docker 主机便是这种情况。 但是，如果使用业务流程协调程序或容器群集，每个容器可能在不同主机（节点）运行，任何节点可能运行任意数目的容器，正如前面的体系结构部分所述。

**通信体系结构**。 eShopOnContainers 应用程序使用两种通信类型，具体取决于功能操作的类型（查询与更新和事务）：

- 通过 API 网关进行的 Http 客户端到微服务通信。 此类型用于查询，以及接受来自客户端应用的更新或事务命令。 使用 API 网关的方法在后面部分中进行详细介绍。

- 基于异步事件的通信。 这种类型通过事件总线发生，以跨微服务传播更新或与外部应用程序集成。 可使用 RabbitMQ 等消息中转站基础结构技术或使用 Azure 服务总线、NServiceBus、MassTransit 或 Brighter 等较高级别（抽象级别）服务总线实现此事件总线。

此应用程序以容器形式，作为一组微服务部署。 客户端应用可以通过 API 网关发布的公共 URL 与作为容器运行的微服务进行通信。

### <a name="data-sovereignty-per-microservice"></a>每个微服务的数据主权

在示例应用程序中，每个微服务拥有其自己的数据库或数据源，不过所有 SQL Server 数据库作为单个容器进行部署。 这种设计的目的是让开发者可轻松地从 GitHub 获取代码、进行克隆，并在 Visual Studio 或 Visual Studio Code 中打开它。 或者可让开发者轻松地使用 .NET Core CLI 和 Docker CLI 编译自定义 Docker 映像，然后在 Docker 开发环境中进行部署和运行。 无论是出于哪种目的，将容器用于数据源，都可让开发者在几分钟内生成和部署，无需预配外部数据库或任何其他严重依赖基础结构（云或本地）的数据源。

在实际生产环境中，为了实现高可用性和可伸缩性，数据库应基于云端或本地数据库服务器，但不是容器。

因此，微服务（甚至此应用程序中的数据库）的部署单元是 Docker 容器，参考应用程序是采用微服务原则的多容器应用程序。

### <a name="additional-resources"></a>其他资源

- **eShopOnContainers GitHub 存储库。参考应用程序的源代码**\
    <https://aka.ms/eShopOnContainers/>

## <a name="benefits-of-a-microservice-based-solution"></a>基于微服务的解决方案的优点

这样的基于微服务的解决方案有许多优点：

**每个微服务相对较小，易于管理和发展**。 具体而言：

- 易于开发者理解和快速提高工作效率。

- 容器启动速度快，从而提高开发者工作效率。

- Visual Studio 这样的 IDE 可以快速加载较小项目，从而提高开发者工作效率。

- 每个微服务可以彼此独立地设计、开发和部署，这可提供灵活性，因为可更轻松地经常部署微服务的新版本。

**可以横向扩展应用程序的各个区域**。 例如，目录服务或购物篮服务可能需要横向扩展，但不需要横向扩展订购流程。 与整体式体系结构相比，微服务基础结构在横向扩展时的资源使用更高效。

**可以在多个团队之间划分开发工作**。 每个服务可以由一个开发团队所有。 每个团队可以独立于其他团队管理、开发、部署和缩放其服务。

**可以更好地隔离问题**。 如果一个服务出现一个问题，最初只影响该服务（除非使用了错误设计，微服务之间有直接依赖项），其他服务可继续处理请求。 与此相反，整体式部署体系结构中的一个异常组件可影响整个系统，尤其是涉及资源（如内存泄露）时。 此外，解决微服务问题后，可仅部署受影响的微服务，而不影响应用程序的其他部分。

**可以使用最新技术**。 由于可开始独立开发服务，然后并行运行这些服务（得益于容器和 .NET Core），可方便地开始使用最新技术和框架，而不受整个应用程序较旧堆栈或框架的限制。

## <a name="downsides-of-a-microservice-based-solution"></a>基于微服务的解决方案的缺点

这样的基于微服务的解决方案有一些缺点：

**分布式应用程序**。 分布式应用程序增加了开发者在设计和生成服务时的难度。 例如，开发者必须使用 HTTP 或 AMPQ 等协议实现服务间通信，这会增加测试和异常处理的复杂性。 还会增加系统延迟。

**部署复杂性**。 如果应用程序具有许多微服务类型，且需要高可伸缩性（需要能为一个服务创建许多实例且在许多主机中实现服务均衡），这意味着 IT 运营和管理需要应对高度部署复杂性。 如果不使用面向微服务的基础结构（如业务流程协调程序和计划程序），为应对增加的复杂性所作的开发工作可能比业务应用程序本身多得多。

**原子事务**。 多个微服务之间的原子事务通常不可能。 业务要求必须接受多个微服务之间的最终一致性。

**增加全局资源需求**（所有服务器或主机的总内存、驱动器和网络资源）。 在许多情况下，如果用微服务方法替代整体式应用程序，新的基于微服务的应用程序所需的初始全局资源数量超过原始整体式应用程序的基础结构需要。 这是因为更高程度的粒度和分布式服务需要更多全局资源。 但是，由于与开发整体式应用程序所需的长期成本相比，资源通常成本较低，且微服务方法具有可横向扩展应用程序特定区域的好处，增加资源使用量好过使用大型、长期应用程序。

**客户端到微服务直接通信的问题**。 对于拥有许多微服务的大型应用程序，如果应用程序需要客户端到微服务直接通信，则存在难题和限制。 一个问题是客户端和每个微服务公开的 API 的需要之间可能存在不匹配。 在某些情况下，客户端应用程序可能需要进行许多单独的请求，以构成 UI，这在 Internet 中效率低下，且在移动网络中不切实际。 因此，仅尽量减少从客户端应用程序到后端系统的请求。

客户端到微服务直接通信的另一个问题是某些微服务可能使用不支持 Web 的协议。 一个服务可能使用二进制协议，而另一个服务可能使用 AMQP 消息。 这些协议不支持防火墙，最好在内部使用。 通常情况下，应用程序应针对防火墙外的通信使用 HTTP 和 WebSockets 等协议。

但是，客户端到服务直接方法的另一个缺点是难以重构这些微服务的协定。 一段时间后，开发者可能需要更改系统分区到服务的方式。 例如，它们可能会合并两个服务或将一个服务拆分为两个或多个服务。 但是，如果客户端直接与服务进行通信，执行这种重构可能会破坏与客户端应用的兼容性。

正如体系结构部分所述，如果基于微服务设计和生成复杂应用程序，需要考虑使用多个细化 API 网关，而不是使用较简单的客户端到微服务直接通信方法。

**微服务分区**。 最后，无论针对微服务体系结构采用哪种方法，另一个难题是确定如何将端到端应用程序分区到多个微服务。 正如本指南的体系结构部分所述，可使用一系列技术和方法。 基本上，需要确定要从其他区域分离的应用程序区域，以及具有较少硬依赖项的区域。 在许多情况下，这与按用例划分的分区服务一致。 例如，在 e-shop 应用程序中，订购服务负责与订购流程相关的所有业务逻辑。 目录服务和购物篮服务则负责实现其他功能。 理想情况下，每个服务应仅具有一小部分职能。 这类似于应用于类的单一职责原则 (SRP)，该原则声明一个类应仅具有一个更改原因。 但我们现在探讨的是微服务，因此范围比单个类要大。 最重要的是，微服务必须是端到端完全自主的，包括其自己数据源的职责。

## <a name="external-versus-internal-architecture-and-design-patterns"></a>外部和内部体系结构和设计模式

外部体系结构是由多个服务构成的微服务体系结构，遵循本指南中体系结构部分所介绍的原则。 但是，根据每个微服务的本质，并独立于你所选择的高级别微服务体系结构，通常建议使用不同的内部体系结构，每个体系结构基于不同的模式，用于不同的微服务。 微服务甚至可以使用不同的技术和编程语言。 图 6-2 反映了此多样性。

![外部体系结构（微服务模式、API 网关、弹性通信、发布/订阅等）和内部体系结构（数据驱动/CRUD、DDD 模式、依赖关系注入、多个库等）之间的区别。](./media/image2.png)

**图 6-2**. 外部和内部体系结构和设计

例如，在 eShopOnContainers  示例中，目录、购物篮和用户个人资料微服务很简单（基本上是 CRUD 子系统）。 因此，其内部体系结构和设计非常简单。 但是，可能还有其他微服务，例如订购微服务，该服务更复杂，体现不断变化的业务规则，具有高度域复杂性。 在这样的情况下，可能需要在特定微服务中实现更高级的模式，正如我们在 eShopOnContainers 订购微服务中采用的、使用域驱动设计 (DDD) 方法定义的模式  。 （我们将在下一部分中了解这些 DDD 模式，下一节介绍 eShopOnContainers 订购微服务的实现  。）

每个微服务采用不同技术的另一个原因是每个微服务的本质。 例如，如果针对 AI 和机器学习域，最好使用功能编程语言，如 F\# 或 R，而不是面向对象编程语言，如 C\#。

底线是每个微服务可基于不同设计模式具有不同内部体系结构。 并非所有微服务都应使用高级 DDD 模式实现，因为这可能会对其过度工程。 类似地，具有不断变化业务逻辑的复杂微服务不应作为 CRUD 组件实现，否则会导致低质量代码。

## <a name="the-new-world-multiple-architectural-patterns-and-polyglot-microservices"></a>新体系：多个体系结构模式和 polyglot 微服务

软件架构师和开发人员使用许多体系结构模式。 以下是一些模式（混合体系结构样式和体系结构模式）：：

- 简单 CRUD、单层级、单层。

- [传统 N 分层](https://docs.microsoft.com/previous-versions/msp-n-p/ee658109(v=pandp.10))。

- [域驱动设计 N 分层](https://blogs.msdn.microsoft.com/cesardelatorre/2011/07/03/published-first-alpha-version-of-domain-oriented-n-layered-architecture-v2-0/)。

- [清洁体系结构](https://8thlight.com/blog/uncle-bob/2012/08/13/the-clean-architecture.html)（用于 [eShopOnWeb](https://aka.ms/WebAppArchitecture)）

- [命令查询职责分离](https://martinfowler.com/bliki/CQRS.html) (CQRS)。

- [事件驱动的体系结构](https://en.wikipedia.org/wiki/Event-driven_architecture) (EDA)。

还可使用许多技术和语言生成微服务，例如 ASP.NET Core Web API、NancyFx、ASP.NET Core SignalR（.NET Core 2 可用）、F\#Node.js、Python、Java, C++、GoLang 等。

请注意，没有适用于所有情况的特定体系结构模式、样式或技术。 图 6-3 显示了一些可用于不同微服务的方法和技术（但不是按照特定顺序）。

![多体系结构模式和 polyglot 微服务意味着可以混合搭配语言和技术以满足每个微服务的需求，并且仍让它们彼此通信。](./media/image3.png)

**图 6-3**。 多体系结构模式和 polyglot 微服务体系

如图 6-3 所示，在由许多微服务（域驱动设计术语中的绑定上下文，或作为自主微服务的“子系统”）构成的应用程序中，可能会采用不同方式实现每个微服务。 每个微服务可能具有不同体系结构模式，使用不同语言和数据库，具体取决于应用程序的本质、业务要求和优先级。 在某些情况下，微服务可能相似。 但这并不常见，因为每个子系统的上下文边界和要求通常不同。

例如，对于简单的 CRUD 维护应用程序，设计和实现 DDD 模式可能无意义。 但对于核心域或核心业务，可能需要应用更高级的模式，以应对不断变化的业务规则的业务复杂性。

尤其是处理由多个子系统构成的大型应用程序时，不应基于单个体系结构模式应用单个顶级体系结构。 例如，CQRS 不应作为整个应用程序的顶级体系结构，但可能适用于一组特定的服务。

没有在任何情况下都通用的体系结构模式。 不可能有“适合所有情况的体系结构模式”。 必须根据每个微服务的优先级，为每个微服务选择不同方法，如以下各节所述。

>[!div class="step-by-step"]
>[上一页](index.md)
>[下一页](data-driven-crud-microservice.md)