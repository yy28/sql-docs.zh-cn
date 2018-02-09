---
title: "CLR 托管环境 |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b3aaf081b264cd74614af93fd58d130b19dfa4d5
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="clr-integration-architecture---clr-hosted-environment"></a>CLR 集成体系结构-CLR 托管环境
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  与 .NET Framework 公共语言运行时 (CLR) 集成的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使数据库程序员可以使用诸如 Visual C#、Visual Basic .NET 和 Visual C++ 等语言。 函数、存储过程、触发器、数据类型和聚合即属于程序员可以用这些语言编写的业务逻辑种类。  
  
  CLR 具有收集垃圾的内存、抢先线程化、元数据服务（类型反射）、代码可验证和代码访问安全性等特点。 CLR 使用元数据来完成以下任务：查找和加载类、在内存中安排实例、解析方法调用、生成本机代码、强制安全性以及设置运行时上下文边界。  
  
 CLR 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 作为运行时环境以不同的方式处理内存、线程和同步。 本主题说明如何集成这两种运行时以便统一管理所有系统资源， 还涉及如何集成 CLR 代码访问安全性 (CAS) 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全性以为用户代码提供安全可靠的执行环境。  
  
## <a name="basic-concepts-of-clr-architecture"></a>CLR 体系结构的基本概念  
 在 .NET Framework 中，程序员使用高级语言实现定义其结构的类（例如，类的字段或属性）和方法。 其中某些方法可能是静态函数。 编译该程序时会生成一个名为程序集的文件以及一个清单，程序集包含用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 中间语言 (MSIL) 编译的代码，清单则包含对依赖程序集的所有引用。  
  
> [!NOTE]  
>  程序集是 CLR 体系结构中的关键元素。 它们是 .NET Framework 中对应用程序代码进行打包、部署和版本化的单位。 通过使用程序集，可以在数据库内部署应用程序代码并以统一方式管理、备份和还原完整的数据库应用程序。  
  
 程序集清单包含有关程序集的元数据，描述在程序中定义的所有结构、字段、属性、类、继承关系、函数和方法。 该清单确定程序集标识，指定组成程序集实现的文件，指定组成程序集的类型和资源，列举对其他程序集的编译时依赖项，并指定确保程序集正常运行所需的权限集。 在运行时使用此信息来解析引用，强制执行版本绑定策略，并验证已加载的程序集的完整性。  
  
 .NET Framework 支持自定义属性，这些属性使用应用程序可以在元数据中捕获的其他信息来对类、属性、函数和方法进行批注。 所有 .NET Framework 编译器不需要解释就可以使用这些批注并将它们作为程序集元数据存储。 可以像检查任何其他元数据那样检查这些批注。  
  
 托管代码是在 CLR 中执行而非直接由操作系统执行的 MSIL。 托管代码应用程序可以获得 CLR 服务，例如自动垃圾收集、运行时类型检查和安全支持等。 这些服务可帮助提供统一和语言-独立于平台的行为的托管的代码应用程序。  
  
## <a name="design-goals-of-clr-integration"></a>CLR 集成的设计目标  
 用户代码在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 CLR 宿主环境（称为 CLR 集成）内运行时，应力求实现以下设计目标：  
  
###### <a name="reliability-safety"></a>可靠性（安全性）  
 不应允许用户代码执行损害数据库引擎进程完整性的操作，例如弹出请求用户响应的消息框或退出进程。 用户代码应不能覆盖数据库引擎内存缓冲区或内部数据结构。  
  
###### <a name="scalability"></a>可伸缩性  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 CLR 具有不同的内部模型，用于计划和内存管理。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持协作、非抢先的线程模型，在此模型中，线程将定期或在等待锁或 I/O 时主动生成执行。 CLR 则支持抢先的线程化模型。 如果在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内运行的用户代码可以直接调用操作系统线程化基元，就不能很好地与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 任务计划程序集成，可能降低系统的可伸缩性。 CLR 不区分虚拟内存和物理内存，但是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 直接管理物理内存并要求在可配置的限制范围内使用物理内存。  
  
 不同的线程化、计划和内存管理的模型给需要支持成千上万的并发用户会话的关系数据库管理系统 (RDBMS) 带来了集成挑战。 体系结构应确保直接调用线程化、内存和同步基元的应用程序编程接口 (API) 的用户代码不损害系统的可伸缩性。  
  
###### <a name="security"></a>Security  
 在数据库中运行的用户代码在访问诸如表和列的数据库对象时，必须遵守 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证和授权规则。 此外，数据库管理员应能从在数据库中运行的用户代码控制对操作系统资源的访问，如文件和网络访问。 这对于托管编程语言很重要，因为与诸如 Transact-SQL 之类的非托管语言不同，托管编程语言提供访问这类资源的 API。 系统必须为用户代码提供安全的方法来访问[!INCLUDE[ssDE](../../includes/ssde-md.md)]进程之外的计算机资源。 有关详细信息，请参阅 [CLR Integration Security](../../relational-databases/clr-integration/security/clr-integration-security.md)。  
  
###### <a name="performance"></a>性能  
 在[!INCLUDE[ssDE](../../includes/ssde-md.md)]中运行的托管用户代码与在服务器外运行的同一代码相比，应具有同等的计算性能。 从托管用户代码进行数据库访问没有本机 [!INCLUDE[tsql](../../includes/tsql-md.md)] 快。 有关详细信息，请参阅[性能的 CLR 集成](../../relational-databases/clr-integration/clr-integration-architecture-performance.md)。  
  
## <a name="clr-services"></a>CLR Services  
 CLR 提供很多服务来帮助实现 CLR 与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 集成的设计目标。  
  
###### <a name="type-safety-verification"></a>类型安全验证  
 类型安全代码是仅以定义完善的方式访问内存结构的代码。 例如，给定有效的对象引用，类型安全代码可以按对应于实际字段成员的固定偏移量来访问内存。 但是，如果代码以任意偏移量访问内存，该偏移量可能超出也可能不超出属于该对象的内存范围，则它就不是类型安全的代码。 在 CLR 中加载程序集时，在使用实时 (JIT) 编译方式编译 MSIL 之前，运行时执行验证阶段，该阶段检查代码以确定其类型是否安全。 成功通过此验证的代码称为可验证的类型安全代码。  
  
###### <a name="application-domains"></a>应用程序域  
 CLR 支持应用程序域作为主机进程内的执行区的概念，在其中可以加载和执行托管代码程序集。 应用程序域边界提供程序集之间的隔离。 根据静态变量和数据成员的可见性以及是否可以动态调用代码对这些程序集进行隔离。 应用程序域也提供加载和卸载代码的机制。 只能通过卸载应用程序域，从内存中卸载代码。 有关详细信息，请参阅[应用程序域和 CLR Integration Security](http://msdn.microsoft.com/library/54ee904e-e21a-4ee7-b4ad-a6f6f71bd473)。  
  
###### <a name="code-access-security-cas"></a>代码访问安全性 (CAS)  
 CLR 安全系统通过给代码分配权限，提供了一种控制托管代码可以执行何种操作的方法。 基于代码标识（例如，程序集的签名或代码的来源）分配代码访问权限。  
  
 CLR 提供了一种可由计算机管理员设置的计算机范围的策略。 此策略为在计算机上运行的所有托管代码定义权限授予方式。 此外，还存在可由宿主（如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]）使用的宿主级安全策略以指定托管代码的其他限制。  
  
 如果 .NET Framework 中的托管 API 公开针对由代码访问权限保护的资源的操作，该 API 在访问资源前将需要该权限。 这将导致 CLR 安全系统触发对调用堆栈中的每个代码单元（程序集）的全面检查。 只有整个调用链具有权限时，才能授予对资源的访问权限。  
  
 请注意在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 CLR 宿主环境内不支持使用 Reflection.Emit API 动态生成托管代码。 此类代码将不具有 CAS 运行权限，因此在运行时会失败。 有关详细信息，请参阅[CLR Integration Code Access Security](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)。  
  
###### <a name="host-protection-attributes-hpas"></a>宿主保护属性 (HPA)  
 CLR 提供一种机制，用于使用宿主 CLR 可能所需的特定属性对属于 .NET Framework 的托管 API 进行批注。 这类属性的示例包括：  
  
-   SharedState，它指示 API 是否公开创建或管理共享状态（例如，静态类字段）的功能。  
  
-   Synchronization，它指示 API 是否公开在线程之间执行同步的功能。  
  
-   ExternalProcessMgmt，它指示 API 是否公开控制主机进程的方法。  
  
 在给定这些属性的基础上，宿主可指定在宿主环境下不允许的 HPA 的列表（如 SharedState 属性）。 在这种情况下，CLR 拒绝用户代码调用某些 API，这些 API 由禁止列表中的 HPA 批注。 有关详细信息，请参阅[宿主保护特性和 CLR 集成编程](../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)。  
  
## <a name="how-sql-server-and-the-clr-work-together"></a>SQL Server 如何与 CLR 协同工作  
 本节介绍 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如何集成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 CLR 的线程化、计划、同步和内存管理模型。 具体而言，本节将在可伸缩性、可靠性和安全性目标方面来介绍集成。 当 CLR 驻留在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实质上是充当 CLR 的操作系统。 CLR 调用由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实现的用于线程化、计划、同步和内存管理的底层例程。 这些基元与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 引擎的其余部分使用的基元相同。 这种方法确保了系统的可伸缩性、可靠性和安全性。  
  
###### <a name="scalability-common-threading-scheduling-and-synchronization"></a>可伸缩性：公共线程化、计划和同步  
 CLR 调用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用于创建线程的 API，以便运行用户代码以及供自己内部使用。 为了在多个线程间同步，CLR 调用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 同步对象。 这使得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计划程序在线程等待某同步对象时可以计划其他任务。 例如，在 CLR 启动垃圾收集时，所有线程均要等待垃圾收集完成。 因为 CLR 线程和它们要等待的同步对象对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计划程序是已知的，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以安排运行不涉及 CLR 的其他数据库任务的线程。 这也使得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以检测由 CLR 同步对象所持有的锁造成的死锁并采用传统技术消除死锁。  
  
 托管代码在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中以抢先方式运行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计划程序可以检测和停止在较长时间内仍未生成的线程。 将 CLR 线程挂钩到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 线程这个功能暗示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计划程序可以标识 CLR 中“逃逸”的线程并管理其优先级。 挂起此类逃逸线程并将它们放回队列中。 在一段规定的时间内不允许运行重复标识为逃逸线程的线程，以便执行其他工作线程。  
  
> [!NOTE]  
>  将自动生成访问数据或分配足够内存来触发垃圾收集的长时间运行的托管代码。 对于不访问数据或分配足够内存来触发垃圾收集的长时间运行的托管代码，应通过调用 .NET Framework 的 System.Thread.Sleep() 函数显式生成它。  
  
###### <a name="scalability-common-memory-management"></a>可伸缩性：公共内存管理  
 CLR 调用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用于分配和取消分配内存的基元。 由于在系统使用的内存总量中考虑了 CLR 使用的内存，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以确保不超过配置的内存限制，并确保 CLR 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不会彼此争用内存。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在系统内存受限制时还可以拒绝 CLR 内存请求，并且在其他任务需要内存时可以请求 CLR 减少内存使用量。  
  
###### <a name="reliability-application-domains-and-unrecoverable-exceptions"></a>可靠性：应用程序域和无法恢复的异常  
 .NET Framework API 中的托管代码遇到严重异常（如内存不足或堆栈溢出）时，并不是总能从这类故障中恢复并确保实现的一致和正确的语义。 这些 API 会引发线程中止异常来应对这类故障。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中驻留时，按以下方式处理这类线程中止：CLR 在发生线程中止的应用程序域中检测所有共享状态。 CLR 通过检查同步对象的存在来做到这点。 如果应用程序域中存在共享状态，则卸载应用程序域本身。 卸载应用程序域将停止当前在该应用程序域中运行的数据库事务。 由于共享状态的存在可能将这类严重异常的影响扩大到触发异常的用户会话之外的其他用户会话，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 CLR 采取了一些措施来减少共享状态出现的可能性。 有关详细信息，请参阅 .NET Framework 文档。  
  
###### <a name="security-permission-sets"></a>安全性：权限集  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允许用户指定部署到数据库的代码的可靠性和安全性要求。 当程序集上载到数据库中时，程序集作者可为该程序集指定以下三个权限集中的一个：SAFE、EXTERNAL_ACCESS 和 UNSAFE。  
  
|||||  
|-|-|-|-|  
|权限集|SAFE|EXTERNAL_ACCESS|UNSAFE|  
|代码访问安全性|仅执行|执行和访问外部资源|“无限制”|  
|编程模型限制|是|是|无限制|  
|可验证性要求|是|用户帐户控制|否|  
|调用本机代码的能力|否|“否”|是|  
  
 SAFE 是最可靠和安全的模式，并且在允许的编程模型方面也具有相关的限制。 给 SAFE 程序集授予了足够的权限，以便运行、执行计算以及访问本地数据库。 SAFE 程序集需要具有可验证的类型安全性，并且不允许调用非托管代码。  
  
 UNSAFE 用于仅能由数据库管理员创建的高度受信任的代码。 这种受信任代码没有代码访问安全性限制，并且可以调用非托管（本机）代码。  
  
 EXTERNAL_ACCESS 提供了一个中间安全选项，允许代码访问数据库外部的资源，而且仍然具有与 SAFE 相同的可靠性。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用主机级 CAS 策略层来设置授予权限的权限集存储在基于三个集之一的主机策略[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目录。 在数据库内运行的托管代码始终获取这些代码访问权限集中的一个。  
  
### <a name="programming-model-restrictions"></a>编程模型限制  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中托管代码的编程模型涉及编写这样的函数、过程和类型：它们一般不需要使用跨多个调用保持的状态或在多个用户会话之间共享状态。 而且，如前文所述，共享状态的存在可导致能够影响应用程序的可伸缩性和可靠性的严重异常。  
  
 出于上述考虑，我们劝阻大家不要使用在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中使用的类的静态变量和静态数据成员。 对于 SAFE 和 EXTERNAL_ACCESS 程序集，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在执行 CREATE ASSEMBLY 时检查程序集的元数据，并在发现使用了静态数据成员和变量时使此类程序集的创建失败。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也可以禁止对使用批注的.NET Framework Api 的调用**SharedState**，**同步**和**ExternalProcessMgmt**宿主保护特性。 这将防止 SAFE 和 EXTERNAL_ACCESS 程序集调用能够启用共享状态、执行同步和影响 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程的完整性的任何 API。 有关详细信息，请参阅[CLR 集成编程模型限制](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)。  
  
## <a name="see-also"></a>另请参阅  
 [CLR 集成安全性](../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [CLR 集成的性能](../../relational-databases/clr-integration/clr-integration-architecture-performance.md)  
  
  
