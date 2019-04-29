---
title: CLR 托管环境 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- type-safe code [CLR integration]
- UNSAFE permission set
- run-time environments [CLR integration]
- common language runtime [SQL Server], about CLR integration
- application domains [CLR integration]
- host protection attributes [CLR integration]
- managed code [SQL Server], common language runtime
- permission sets [CLR integration]
- reliability [CLR integration]
- SAFE permission set
- code access security [CLR integration]
- EXTERNAL_ACCESS permission set
- verifying type safety
- scalability [CLR integration]
- hosted environments [CLR integration]
- HPAs [CLR integration]
ms.assetid: d280d359-08f0-47b5-a07e-67dd2a58ad73
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: dbbc884a32f892830ec4b7b66e3a67c45fc37416
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62922561"
---
# <a name="clr-hosted-environment"></a>CLR 宿主环境
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 公共语言运行时 (CLR) 是执行很多现代编程语言的环境，这些语言包括 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 和 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C++。 CLR 具有收集垃圾的内存、抢先线程化、元数据服务（类型反射）、代码可验证和代码访问安全性等特点。 CLR 使用元数据来完成以下任务：查找和加载类、在内存中安排实例、解析方法调用、生成本机代码、强制安全性以及设置运行时上下文边界。  
  
 CLR 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 作为运行时环境以不同的方式处理内存、线程和同步。 本主题说明如何集成这两种运行时以便统一管理所有系统资源， 还涉及如何集成 CLR 代码访问安全性 (CAS) 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安全性以为用户代码提供安全可靠的执行环境。  
  
## <a name="basic-concepts-of-clr-architecture"></a>CLR 体系结构的基本概念  
 在 .NET Framework 中，程序员使用高级语言实现定义其结构的类（例如，类的字段或属性）和方法。 其中某些方法可能是静态函数。 编译该程序时会生成一个名为程序集的文件以及一个清单，程序集包含用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 中间语言 (MSIL) 编译的代码，清单则包含对依赖程序集的所有引用。  
  
> [!NOTE]  
>  程序集是 CLR 体系结构中的关键元素。 它们是 .NET Framework 中对应用程序代码进行打包、部署和版本化的单位。 通过使用程序集，可以在数据库内部署应用程序代码并以统一方式管理、备份和还原完整的数据库应用程序。  
  
 程序集清单包含有关程序集的元数据，描述在程序中定义的所有结构、字段、属性、类、继承关系、函数和方法。 该清单确定程序集标识，指定组成程序集实现的文件，指定组成程序集的类型和资源，列举对其他程序集的编译时依赖项，并指定确保程序集正常运行所需的权限集。 在运行时使用此信息来解析引用，强制执行版本绑定策略，并验证已加载的程序集的完整性。  
  
 .NET Framework 支持自定义属性，这些属性使用应用程序可以在元数据中捕获的其他信息来对类、属性、函数和方法进行批注。 所有 .NET Framework 编译器不需要解释就可以使用这些批注并将它们作为程序集元数据存储。 可以像检查任何其他元数据那样检查这些批注。  
  
 托管代码是在 CLR 中执行而非直接由操作系统执行的 MSIL。 托管代码应用程序可以获得 CLR 服务，例如自动垃圾收集、运行时类型检查和安全支持等。 这些服务帮助提供统一的平台和语言独立的托管的代码应用程序的行为。  
  
## <a name="design-goals-of-clr-integration"></a>CLR 集成的设计目标  
 用户代码在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的 CLR 宿主环境（称为 CLR 集成）内运行时，应力求实现以下设计目标：  
  
###### <a name="reliability-safety"></a>可靠性（安全性）  
 不应允许用户代码执行损害数据库引擎进程完整性的操作，例如弹出请求用户响应的消息框或退出进程。 用户代码应不能覆盖数据库引擎内存缓冲区或内部数据结构。  
  
###### <a name="scalability"></a>可伸缩性  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 和 CLR 具有用于计划和内存管理的不同内部模型。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持协作、非抢先的线程模型，在此模型中，线程将定期或在等待锁或 I/O 时主动生成执行。 CLR 则支持抢先的线程化模型。 如果在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内运行的用户代码可以直接调用操作系统线程化基元，就不能很好地与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 任务计划程序集成，可能降低系统的可伸缩性。 CLR 不区分虚拟内存和物理内存，但是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 直接管理物理内存并要求在可配置的限制范围内使用物理内存。  
  
 不同的线程化、计划和内存管理的模型给需要支持成千上万的并发用户会话的关系数据库管理系统 (RDBMS) 带来了集成挑战。 体系结构应确保直接调用线程化、内存和同步基元的应用程序编程接口 (API) 的用户代码不损害系统的可伸缩性。  
  
###### <a name="security"></a>安全性  
 在数据库中运行的用户代码在访问诸如表和列的数据库对象时，必须遵守 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证和授权规则。 此外，数据库管理员应能从在数据库中运行的用户代码控制对操作系统资源的访问，如文件和网络访问。 这对于托管编程语言很重要，因为与诸如 Transact-SQL 之类的非托管语言不同，托管编程语言提供访问这类资源的 API。 系统必须为用户代码提供安全的方法来访问[!INCLUDE[ssDE](../../../includes/ssde-md.md)]进程之外的计算机资源。 有关详细信息，请参阅 [CLR Integration Security](security/clr-integration-security.md)。  
  
###### <a name="performance"></a>性能  
 在[!INCLUDE[ssDE](../../../includes/ssde-md.md)]中运行的托管用户代码与在服务器外运行的同一代码相比，应具有同等的计算性能。 从托管用户代码进行数据库访问没有本机 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 快。 有关详细信息，请参阅[CLR 集成性能](clr-integration-architecture-performance.md)。  
  
## <a name="clr-services"></a>CLR Services  
 CLR 提供很多服务来帮助实现 CLR 与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 集成的设计目标。  
  
###### <a name="type-safety-verification"></a>类型安全验证  
 类型安全代码是仅以定义完善的方式访问内存结构的代码。 例如，给定有效的对象引用，类型安全代码可以按对应于实际字段成员的固定偏移量来访问内存。 但是，如果代码以任意偏移量访问内存，该偏移量可能超出也可能不超出属于该对象的内存范围，则它就不是类型安全的代码。 在 CLR 中加载程序集时，在使用实时 (JIT) 编译方式编译 MSIL 之前，运行时执行验证阶段，该阶段检查代码以确定其类型是否安全。 成功通过此验证的代码称为可验证的类型安全代码。  
  
###### <a name="application-domains"></a>应用程序域  
 CLR 支持应用程序域作为主机进程内的执行区的概念，在其中可以加载和执行托管代码程序集。 应用程序域边界提供程序集之间的隔离。 根据静态变量和数据成员的可见性以及是否可以动态调用代码对这些程序集进行隔离。 应用程序域也提供加载和卸载代码的机制。 只能通过卸载应用程序域，从内存中卸载代码。 有关详细信息，请参阅[应用程序域和 CLR 集成安全性](../../database-engine/dev-guide/application-domains-and-clr-integration-security.md)。  
  
###### <a name="code-access-security-cas"></a>代码访问安全性 (CAS)  
 CLR 安全系统通过给代码分配权限，提供了一种控制托管代码可以执行何种操作的方法。 基于代码标识（例如，程序集的签名或代码的来源）分配代码访问权限。  
  
 CLR 提供了一种可由计算机管理员设置的计算机范围的策略。 此策略为在计算机上运行的所有托管代码定义权限授予方式。 此外，还存在可由宿主（如 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]）使用的宿主级安全策略以指定托管代码的其他限制。  
  
 如果 .NET Framework 中的托管 API 公开针对由代码访问权限保护的资源的操作，该 API 在访问资源前将需要该权限。 这将导致 CLR 安全系统触发对调用堆栈中的每个代码单元（程序集）的全面检查。 只有整个调用链具有权限时，才能授予对资源的访问权限。  
  
 请注意在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 CLR 宿主环境内不支持使用 Reflection.Emit API 动态生成托管代码。 此类代码将不具有 CAS 运行权限，因此在运行时会失败。 有关详细信息，请参阅[CLR 集成代码访问安全性](security/clr-integration-code-access-security.md)。  
  
###### <a name="host-protection-attributes-hpas"></a>宿主保护属性 (HPA)  
 CLR 提供一种机制，用于使用宿主 CLR 可能所需的特定属性对属于 .NET Framework 的托管 API 进行批注。 这类属性的示例包括：  
  
-   SharedState，它指示 API 是否公开创建或管理共享状态（例如，静态类字段）的功能。  
  
-   Synchronization，它指示 API 是否公开在线程之间执行同步的功能。  
  
-   ExternalProcessMgmt，它指示 API 是否公开控制主机进程的方法。  
  
 在给定这些属性的基础上，宿主可指定在宿主环境下不允许的 HPA 的列表（如 SharedState 属性）。 在这种情况下，CLR 拒绝用户代码调用某些 API，这些 API 由禁止列表中的 HPA 批注。 有关详细信息，请参阅[宿主保护属性和 CLR 集成编程](../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)。  
  
## <a name="how-sql-server-and-the-clr-work-together"></a>SQL Server 如何与 CLR 协同工作  
 本节介绍 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 如何集成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 和 CLR 的线程化、计划、同步和内存管理模型。 具体而言，本节将在可伸缩性、可靠性和安全性目标方面来介绍集成。 当 CLR 驻留在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内部时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实质上是充当 CLR 的操作系统。 CLR 调用由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实现的用于线程化、计划、同步和内存管理的底层例程。 这些基元与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 引擎的其余部分使用的基元相同。 这种方法确保了系统的可伸缩性、可靠性和安全性。  
  
###### <a name="scalability-common-threading-scheduling-and-synchronization"></a>可伸缩性：常见线程、 计划和同步  
 CLR 调用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用于创建线程的 API，以便运行用户代码以及供自己内部使用。 为了在多个线程间同步，CLR 调用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 同步对象。 这使得 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 计划程序在线程等待某同步对象时可以计划其他任务。 例如，在 CLR 启动垃圾收集时，所有线程均要等待垃圾收集完成。 因为 CLR 线程和它们要等待的同步对象对于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 计划程序是已知的，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以安排运行不涉及 CLR 的其他数据库任务的线程。 这也使得 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以检测由 CLR 同步对象所持有的锁造成的死锁并采用传统技术消除死锁。  
  
 托管代码在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中以抢先方式运行。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 计划程序可以检测和停止在较长时间内仍未生成的线程。 将 CLR 线程挂钩到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 线程这个功能暗示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 计划程序可以标识 CLR 中“逃逸”的线程并管理其优先级。 挂起此类逃逸线程并将它们放回队列中。 在一段规定的时间内不允许运行重复标识为逃逸线程的线程，以便执行其他工作线程。  
  
> [!NOTE]  
>  将自动生成访问数据或分配足够内存来触发垃圾收集的长时间运行的托管代码。 对于不访问数据或分配足够内存来触发垃圾收集的长时间运行的托管代码，应通过调用 .NET Framework 的 System.Thread.Sleep() 函数显式生成它。  
  
###### <a name="scalability-common-memory-management"></a>可伸缩性：常见的内存管理  
 CLR 调用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用于分配和取消分配内存的基元。 由于在系统使用的内存总量中考虑了 CLR 使用的内存，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以确保不超过配置的内存限制，并确保 CLR 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不会彼此争用内存。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 在系统内存受限制时还可以拒绝 CLR 内存请求，并且在其他任务需要内存时可以请求 CLR 减少内存使用量。  
  
###### <a name="reliability-application-domains-and-unrecoverable-exceptions"></a>可靠性：应用程序域和无法恢复的异常  
 .NET Framework API 中的托管代码遇到严重异常（如内存不足或堆栈溢出）时，并不是总能从这类故障中恢复并确保实现的一致和正确的语义。 这些 API 会引发线程中止异常来应对这类故障。  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中驻留时，按以下方式处理这类线程中止：CLR 在发生线程中止的应用程序域中检测所有共享状态。 CLR 通过检查同步对象的存在来做到这点。 如果应用程序域中存在共享状态，则卸载应用程序域本身。 卸载应用程序域将停止当前在该应用程序域中运行的数据库事务。 由于共享状态的存在可能将这类严重异常的影响扩大到触发异常的用户会话之外的其他用户会话，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 和 CLR 采取了一些措施来减少共享状态出现的可能性。 有关详细信息，请参阅 .NET Framework 文档。  
  
###### <a name="security-permission-sets"></a>安全性：权限集  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 允许用户指定部署到数据库中的代码的可靠性和安全性要求。 当程序集上传到数据库时，程序集的作者可以指定三个权限集之一该程序集：安全的 EXTERNAL_ACCESS 和 UNSAFE。  
  
|||||  
|-|-|-|-|  
|权限集|SAFE|EXTERNAL_ACCESS|UNSAFE|  
|代码访问安全性|仅执行|执行和访问外部资源|“无限制”|  
|编程模型限制|是|是|无限制|  
|可验证性要求|是|是|否|  
|调用本机代码的能力|否|否|是|  
  
 SAFE 是最可靠和安全的模式，并且在允许的编程模型方面也具有相关的限制。 给 SAFE 程序集授予了足够的权限，以便运行、执行计算以及访问本地数据库。 SAFE 程序集需要具有可验证的类型安全性，并且不允许调用非托管代码。  
  
 UNSAFE 用于仅能由数据库管理员创建的高度受信任的代码。 这种受信任代码没有代码访问安全性限制，并且可以调用非托管（本机）代码。  
  
 EXTERNAL_ACCESS 提供了一个中间安全选项，允许代码访问数据库外部的资源，而且仍然具有与 SAFE 相同的可靠性。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用宿主级 CAS 策略层设置宿主策略，该宿主策略根据存储在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 目录中的权限集授予三个权限集之一。 在数据库内运行的托管代码始终获取这些代码访问权限集中的一个。  
  
### <a name="programming-model-restrictions"></a>编程模型限制  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中托管代码的编程模型涉及编写这样的函数、过程和类型：它们一般不需要使用跨多个调用保持的状态或在多个用户会话之间共享状态。 而且，如前文所述，共享状态的存在可导致能够影响应用程序的可伸缩性和可靠性的严重异常。  
  
 出于上述考虑，我们劝阻大家不要使用在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中使用的类的静态变量和静态数据成员。 对于 SAFE 和 EXTERNAL_ACCESS 程序集，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 在执行 CREATE ASSEMBLY 时检查程序集的元数据，并在发现使用了静态数据成员和变量时使此类程序集的创建失败。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 还不允许调用使用 `SharedState`、`Synchronization` 和 `ExternalProcessMgmt` 宿主保护属性批注的 .NET Framework API。 这将防止 SAFE 和 EXTERNAL_ACCESS 程序集调用能够启用共享状态、执行同步和影响 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 进程的完整性的任何 API。 有关详细信息，请参阅[CLR 集成编程模型限制](database-objects/clr-integration-programming-model-restrictions.md)。  
  
## <a name="see-also"></a>请参阅  
 [CLR 集成安全性](security/clr-integration-security.md)   
 [CLR 集成的性能](clr-integration-architecture-performance.md)  
  
  
