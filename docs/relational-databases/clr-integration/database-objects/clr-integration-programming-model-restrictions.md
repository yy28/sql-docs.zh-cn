---
title: CLR 集成编程模型限制 |Microsoft Docs
description: SQL Server 在托管数据库对象上首次使用 CREATE ASSEMBLY 和在运行时执行代码检查。
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
ms.openlocfilehash: f5f04017124520f6e2acd0669946d5d43d4e83f4
ms.sourcegitcommit: 21c14308b1531e19b95c811ed11b37b9cf696d19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2020
ms.locfileid: "86160165"
---
# <a name="clr-integration-programming-model-restrictions"></a>CLR 集成编程模型限制
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/applies-to-version/sql-asdbmi.md)]
  在生成托管存储过程或其他托管数据库对象时，需要考虑执行某些代码检查 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]当第一次在数据库中注册时，使用**CREATE assembly**语句并在运行时对托管代码程序集执行检查。 在运行时也将检查托管代码，这是因为在程序集中，也许存在在运行时实际上可能永远无法访问的代码路径。  这样一来，在注册第三方程序集时尤其灵活，因为，当存在专门在客户端环境下运行而从不在承载的 CLR 中执行的“不安全”代码时，不会阻塞程序集。 托管代码必须满足的要求取决于该程序集是注册为**安全**的、 **EXTERNAL_ACCESS**的、**不**安全的 **、最**严格的，并在下面列出。  
  
 除了对托管代码程序集进行了限制，还授予了一些代码安全权限。 公共语言运行时 (CLR) 支持称为代码访问安全性 (CAS) 的托管代码安全模式。 在这种模式下，根据代码的标识来对程序集授予权限。 **SAFE**、 **EXTERNAL_ACCESS**和**UNSAFE**程序集具有不同的 CAS 权限。 有关详细信息，请参阅[CLR 集成代码访问安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)。  
  
## <a name="create-assembly-checks"></a>CREATE ASSEMBLY 检查  
 当运行**CREATE ASSEMBLY**语句时，将对每个安全级别执行以下检查。  如果任何检查失败， **CREATE ASSEMBLY**将失败并出现错误消息。  
  
### <a name="global-any-security-level"></a>全局（任何安全级别）  
 所有被引用的程序集都必须满足下列一个或多个条件：  
  
-   程序集已在数据库中注册。  
  
-   程序集是受支持的程序集之一。 有关详细信息，请参阅[支持的 .NET Framework 库](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)。  
  
-   你使用的是中的**CREATE ASSEMBLY**_ \<location> ，_ 并且所有引用的程序集及其依赖项在中均可用 *\<location>* 。  
  
-   你使用的是**中的 CREATE ASSEMBLY**_ \<bytes ...> ，_ 所有引用都是通过以空格分隔的字节来指定的。  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 所有**EXTERNAL_ACCESS**程序集都必须满足以下条件：  
  
-   静态字段不用来存储信息。 允许只读静态字段。  
  
-   PEVerify 测试通过。 PEVerify 工具 (peverify.exe) 随 .NET Framework SDK 一起提供，该工具可检查 MSIL 代码及关联元数据是否满足类型安全要求。  
  
-   不使用同步，例如，使用**system.runtime.remoting.contexts.synchronizationattribute>** 类。  
  
-   不使用终结器方法。  
  
 **EXTERNAL_ACCESS**程序集中不允许以下自定义属性：  
  
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
  
-   检查所有**EXTERNAL_ACCESS**的程序集条件。  
  
## <a name="runtime-checks"></a>运行时检查  
 在运行时，将针对下列条件检查代码程序集。 如果发现任何一个条件，则将不允许托管代码运行，且将会引发异常。  
  
### <a name="unsafe"></a>UNSAFE  
 加载程序集-可以通过从字节数组中调用 system.exception **（）** 方法或通过使用反射隐式方式进行显式加载。**发出**命名空间-不允许。  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 检查所有**不安全**条件。  
  
 在支持的程序集列表中不允许所有使用以下宿主保护属性 (HPA) 值批注的类型和方法。  
  
-   SelfAffectingProcessMgmt  
  
-   SelfAffectingThreading  
  
-   同步  
  
-   SharedState  
  
-   ExternalProcessMgmt  
  
-   ExternalThreading  
  
-   SecurityInfrastructure  
  
-   MayLeakOnAbort  
  
-   UI  
  
 有关 Hpa 的详细信息以及支持的程序集中不允许的类型和成员的列表，请参阅[宿主保护属性和 CLR 集成编程](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)。  
  
### <a name="safe"></a>SAFE  
 检查所有**EXTERNAL_ACCESS**条件。  
  
## <a name="see-also"></a>另请参阅  
 [支持的 .NET Framework 库](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)   
 [CLR 集成代码访问安全性](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [宿主保护属性和 CLR 集成编程](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [创建程序集](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
