---
title: CLR 集成编程模型限制 |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], programming model restrictions
- assemblies [CLR integration], CREATE ASSEMBLY checks
- programming model restrictions [CLR integration]
- assemblies [CLR integration], runtime checks
ms.assetid: 2446afc2-9d21-42d3-9847-7733d3074de9
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d9d42017e3dfd6016d8b4a42c6953905e804200f
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54136017"
---
# <a name="clr-integration-programming-model-restrictions"></a>CLR 集成编程模型限制
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在生成托管存储的过程或其他托管的数据库对象，在某些执行代码检查[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，需要考虑。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 托管的代码程序集执行检查时首次将其注册在数据库中，使用**CREATE ASSEMBLY**语句，并且还在运行时。 在运行时也将检查托管代码，这是因为在程序集中，也许存在在运行时实际上可能永远无法访问的代码路径。  这样一来，在注册第三方程序集时尤其灵活，因为，当存在专门在客户端环境下运行而从不在承载的 CLR 中执行的“不安全”代码时，不会阻塞程序集。 托管的代码必须满足的要求取决于是否作为注册的程序集**安全**， **EXTERNAL_ACCESS**，或**UNSAFE**，**安全**是最严格的并在下方列出。  
  
 除了对托管代码程序集进行了限制，还授予了一些代码安全权限。 公共语言运行时 (CLR) 支持称为代码访问安全性 (CAS) 的托管代码安全模式。 在这种模式下，根据代码的标识来对程序集授予权限。 **安全**， **EXTERNAL_ACCESS**，和**UNSAFE**程序集具有不同的 CAS 权限。 有关详细信息，请参阅[CLR 集成代码访问安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)。  
  
## <a name="create-assembly-checks"></a>CREATE ASSEMBLY 检查  
 当**CREATE ASSEMBLY**运行语句时，为每个安全级别执行以下检查。  如果有任何检查失败， **CREATE ASSEMBLY**将失败并显示错误消息。  
  
### <a name="global-any-security-level"></a>全局（任何安全级别）  
 所有被引用的程序集都必须满足下列一个或多个条件：  
  
-   程序集已在数据库中注册。  
  
-   程序集是受支持的程序集之一。 有关详细信息，请参阅[支持的.NET Framework 库](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)。  
  
-   正在使用**创建程序集从**_\<位置 >，_ 和中提供了所有引用的程序集和其依赖项*\<位置 >*.  
  
-   正在使用**创建程序集从**_\<字节...>，_ 和所有引用指定通过空格分隔的字节。  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 所有**EXTERNAL_ACCESS**程序集都必须满足以下条件：  
  
-   静态字段不用来存储信息。 允许只读静态字段。  
  
-   PEVerify 测试通过。 PEVerify 工具 (peverify.exe) 随 .NET Framework SDK 一起提供，该工具可检查 MSIL 代码及关联元数据是否满足类型安全要求。  
  
-   同步，例如，使用**SynchronizationAttribute**类，则不使用。  
  
-   不使用终结器方法。  
  
 以下自定义属性中不允许**EXTERNAL_ACCESS**程序集：  
  
-   System.ContextStaticAttribute  
  
-   System.MTAThreadAttribute  
  
-   System.Runtime.CompilerServices.MethodImplAttribute  
  
-   System.Runtime.CompilerServices.CompilationRelaxationsAttribute  
  
-   System.Runtime.Remoting.Contexts.ContextAttribute  
  
-   System.Runtime.Remoting.Contexts.SynchronizationAttribute  
  
-   System.Runtime.InteropServices.DllImportAttribute  
  
-   System.Security.Permissions.CodeAccessSecurityAttribute  
  
-   System.Security.SuppressUnmanagedCodeSecurityAttribute  
  
-   System.Security.UnverifiableCodeAttribute  
  
-   System.STAThreadAttribute  
  
-   System.ThreadStaticAttribute  
  
### <a name="safe"></a>SAFE  
  
-   所有**EXTERNAL_ACCESS**检查程序集条件。  
  
## <a name="runtime-checks"></a>运行时检查  
 在运行时，将针对下列条件检查代码程序集。 如果发现任何一个条件，则将不允许托管代码运行，且将会引发异常。  
  
### <a name="unsafe"></a>UNSAFE  
 通过调用显式加载程序集**System.Reflection.Assembly.Load()** 方法从字节数组，或通过使用隐式**Reflection.Emit**命名空间-不允许。  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 所有**UNSAFE**检查条件。  
  
 在支持的程序集列表中不允许所有使用以下宿主保护属性 (HPA) 值批注的类型和方法。  
  
-   SelfAffectingProcessMgmt  
  
-   SelfAffectingThreading  
  
-   Synchronization  
  
-   SharedState  
  
-   ExternalProcessMgmt  
  
-   ExternalThreading  
  
-   SecurityInfrastructure  
  
-   MayLeakOnAbort  
  
-   UI  
  
 有关 Hpa 以及不允许的类型和受支持的程序集中的成员的列表的详细信息，请参阅[宿主保护属性和 CLR 集成编程](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)。  
  
### <a name="safe"></a>SAFE  
 所有**EXTERNAL_ACCESS**检查条件。  
  
## <a name="see-also"></a>请参阅  
 [支持的.NET Framework 库](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)   
 [CLR 集成代码访问安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [宿主保护属性和 CLR 集成编程](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [创建程序集](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
