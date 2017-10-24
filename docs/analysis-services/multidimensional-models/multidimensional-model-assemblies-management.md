---
title: "多维模型程序集管理 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permissions [Analysis Services], assemblies
- calling user-defined functions
- user impersonation [Analysis Services]
- impersonation [Analysis Services]
- Data Mining Extensions [Analysis Services], assemblies
- MDX [Analysis Services], assemblies
- user-defined functions [Analysis Services]
- Analysis Services objects, assemblies
- assemblies [Analysis Services]
- application domains [Analysis Services]
ms.assetid: b2645d10-6d17-444e-9289-f111ec48bbfb
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 38bbf72a7fd58be5db3d8672de1ad4269c763020
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="multidimensional-model-assemblies-management"></a>多维模型程序集管理
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供了一些可用于多维表达式 (MDX) 和数据挖掘扩展插件 (DMX) 语言的内部函数，这些内部函数经过专门设计，可用于完成从标准统计计算到遍历层次结构中的成员的所有任务。 但是，任何复杂且健壮的产品都需要不断地扩展其功能，本产品也不例外。  
  
 因此，通过 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，您可以将程序集添加到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例或数据库。 使用程序集，您可以使用任何公共语言运行时 (CLR) 语言（如 Microsoft Visual Basic .NET 或 Microsoft Visual C#）来创建用户定义的外部函数。 还可以使用组件对象模型 (COM) 自动化语言，如 Microsoft Visual Basic 或 Microsoft Visual C++。  
  
> [!IMPORTANT]  
>  COM 程序集可能会造成安全风险。 由于此风险和其他注意事项， [!INCLUDE[ssASversion10](../../includes/ssasversion10-md.md)]中不推荐使用 COM 程序集。 未来版本可能不支持 COM 程序集。  
  
 使用程序集可以扩展 MDX 和 DMX 的业务功能。 应当在诸如动态链接库 (DLL) 这样的库中构建所需的功能，然后将库作为程序集添加到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。 然后，库中的公共方法对 MDX 和 DMX 表达式、过程、计算、操作和客户端应用程序显示为用户定义函数。  
  
 可向服务器添加具有新过程和新功能的程序集。 您可以使用程序集增强或添加服务器未提供的自定义功能。 您还可以通过使用程序集，向多维表达式 (MDX)、数据挖掘扩展 (DMX) 或存储过程添加新功能。 可从运行自定义应用程序处加载程序集，并且程序集二进制文件的副本将和数据库数据一起保存到服务器中。 删除程序集时，程序集副本也会从服务器中删除。  
  
 程序集可为两种不同的类型：COM 和 CLR。 CLR 程序集是使用 .NET Framework 编程语言（如 C#、Visual Basic .NET 和托管 C++）开发的程序集。 COM 程序集是必须在服务器中注册的 COM 库。  
  
 可以将程序集添加到 <xref:Microsoft.AnalysisServices.Server> 或 <xref:Microsoft.AnalysisServices.Database> 对象。 连接到服务器的任何用户或服务器中任何对象均可以调用服务器程序集。 但数据库程序集却只能由连接到 <xref:Microsoft.AnalysisServices.Database> 的数据库对象或用户调用。  
  
 简单 <xref:Microsoft.AnalysisServices.Assembly> 对象由基本信息（名称和 ID）、文件集合和安全规范组成。  
  
 如果调试文件是和程序集文件一起加载的，则文件集合指已加载程序集文件及其相应调试文件 (.pdb)。 程序集文件可从应用程序定义该文件处进行加载，并且其副本将和数据一起保存到服务器中。 程序集文件的副本可用于在每次启动服务时加载程序集。  
  
 安全规范包括用于运行程序集的权限集和模拟。  
  
## <a name="calling-user-defined-functions"></a>调用用户定义函数  
 调用程序集中用户定义函数的过程就像调用内部函数一样，但必须使用完全限定名称。 例如，MDX 查询中包含一个返回 MDX 所需类型的用户定义函数，如下例所示：  
  
```  
Select MyAssembly.MyClass.MyStoredProcedure(a, b, c) on 0 from Sales  
```  
  
 用户定义函数也可以使用 CALL 关键字调用。 必须对返回记录集或 void 值的用户定义函数使用 CALL 关键字，并且如果用户定义函数依赖于 MDX 或 DMX 语句或脚本（如当前多维数据集或数据挖掘模型）上下文中的对象，则不能使用 CALL 关键字。 在 MDX 或 DMX 查询之外调用函数的通常做法是使用 AMO 对象模型执行管理功能。 例如，如果想要在 MDX 语句中使用 `MyVoidProcedure(a, b, c)` 函数，可采用下面的语法：  
  
```  
Call MyAssembly.MyClass.MyVoidProcedure(a, b, c)  
```  
  
 程序集通过一次性地开发通用代码并将其存储在某个位置，使数据库开发过程得到了简化。 客户端软件开发人员可以创建 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的函数库，并通过其应用程序对这些库进行分发。  
  
 程序集和用户定义函数可以复制 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 函数库或其他程序集的函数名称。 只要用完全限定名称调用用户定义函数， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就会使用正确的步骤。 出于安全目的，并为了防止调用不同类库中的重复名称， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 要求对存储过程仅使用完全限定名称。  
  
 若要从特定 CLR 程序集调用用户定义函数，用户定义函数前面必须有程序集名称、完整类名称和过程名称，如下所示：  
  
 *AssemblyName*.*FullClassName*.*ProcedureName*(*Argument1*, *Argument2*, ...)  
  
 为了保持对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]早期版本的向后兼容，下面的语法也可以接受：  
  
 *AssemblyName*!*FullClassName*!*ProcedureName*(*Argument1*, *Argument2*, ...)  
  
 如果 COM 库支持多个接口，则接口 ID 还可用于解析过程名称，如下所示：  
  
 *AssemblyName*!*InterfaceID*!*ProcedureName*(*Argument1*, *Argument2*, ...)  
  
## <a name="security"></a>Security  
 程序集的安全性基于 .NET Framework 安全模式，这是一个代码访问安全模式。 .NET Framework 支持代码访问安全机制，此机制假设：运行时可承载完全可信和部分可信的代码。 .NET Framework 代码访问安全性所保护的资源通常由要求具有相应权限才能访问资源的托管代码所包装。 仅当调用堆栈中的所有调用方（在程序集层）均具有相应资源权限时，此权限要求才得到满足。  
  
 对于程序集，执行权限随 **PermissionSet** 对象的 **Assembly** 属性传递。 托管代码接收的权限由有效的安全策略确定。 非[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 宿主环境中已有三个有效的策略级别：企业、计算机和用户。 代码接收的有效权限列表由这三个级别获得的权限交集所确定。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 如果是 CLR 的宿主，它将为其提供宿主级别的安全策略级别，此策略是低于始终有效的三个策略级别的附加策略级别。 会为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]创建的每个应用程序域设置此策略。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 宿主级别策略组合了用于系统程序集的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 固定策略和用于用户程序集的用户指定策略。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 宿主策略的用户指定部分基于程序集所有者，此所有者将为每个程序集指定三个权限存储桶中的一个：  
  
|权限设置|Description|  
|------------------------|-----------------|  
|**Safe**|提供内部计算权限。 此权限存储桶不分配访问 .NET Framework 中任何受保护资源的权限。 如果没有对 **PermissionSet** 属性指定任何权限存储桶，则这是程序集的默认权限存储桶。|  
|**ExternalAccess**|提供和 **Safe** 设置相同的访问权限，以及访问外部系统资源的附加功能。 此权限存储桶无法保证安全性（尽管有可能保证这种情况的安全），但可以保证可靠性。|  
|**Unsafe**|无限制。 对运行于此权限集下的托管代码无法提供安全性或可靠性保证。 任何权限，甚至管理员提供的自定义权限都将授予在此信任级别运行的代码。|  
  
 当 CLR 由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]承载时，基于堆栈审核的权限检查在本机 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 代码的边界停止。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 程序集中的任何托管代码始终属于前面列出的三种权限类别中的一种。  
  
 COM（或非托管）程序集例程不支持 CLR 安全模式。  
  
### <a name="impersonation"></a>模拟  
 无论托管代码何时访问 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]外的任何资源， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 都将遵守与 **ImpersonationMode** 程序集属性设置相关的规则，以确保访问在适当的 Windows 安全性上下文中进行。 由于使用 **Safe** 权限设置的程序集不能访问 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]外的资源，所以这些规则仅适用于使用 **ExternalAccess** 和 **Unsafe** 权限设置的程序集。  
  
-   如果当前执行的上下文对应于通过 Windows 身份验证的登录，并且和原始调用方的上下文相同（即中间没有 EXECUTE AS），则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将在访问资源之前模拟通过 Windows 身份验证的登录。  
  
-   如果某个中间 EXECUTE AS 更改了执行上下文，使之不再是原始调用方的上下文，则访问外部资源的尝试将失败。  
  
 **ImpersonationMode** 属性可设置为 **ImpersonateCurrentUser** 或 **ImpersonateAnonymous**。 默认设置 **ImpersonateCurrentUser**在当前用户的网络登录帐户下运行程序集。 如果使用 **ImpersonateAnonymous** 设置，则执行上下文对应于服务器上的 Windows 登录用户帐户 IUSER_servername。 这是 Internet guest 帐户，在服务器上只有有限的权限。 在此上下文中运行的程序集只能访问本地服务器上的有限资源。  
  
### <a name="application-domains"></a>应用程序域  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 不直接显示应用程序域。 由于一组程序集运行于同一个应用程序域中，因此应用程序域可以在执行期间使用 .NET Framework 中的 **System.Reflection** 命名空间或以其他方式发现彼此，并且可以用后期绑定的方式调用这些程序集。 此类调用将受到基于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 授权的安全性所使用的权限检查的约束。  
  
 不应依赖于在同一应用程序域中查找程序集，因为应用程序域边界和每个域中的程序集都是由此实现而定义的。  
  
## <a name="see-also"></a>另请参阅  
 [设置存储过程的安全性](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/setting-security-for-stored-procedures.md)   
 [定义存储过程](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  

