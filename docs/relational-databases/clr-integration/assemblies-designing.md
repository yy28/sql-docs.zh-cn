---
title: 设计程序集 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- designing assemblies [SQL Server]
- assemblies [CLR integration], designing
ms.assetid: 9c07f706-6508-41aa-a4d7-56ce354f9061
author: rothja
ms.author: jroth
ms.openlocfilehash: 205347e9d70ae378e10245c45d2580767eafbd8c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028036"
---
# <a name="assemblies---designing"></a>程序集 - 设计
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题说明了设计程序集时应考虑的下列因素：  
  
-   打包程序集  
  
-   管理程序集安全性  
  
-   对程序集的限制  
  
## <a name="packaging-assemblies"></a>打包程序集  
 程序集可以在其类和方法中包含多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 例程或类型的功能。 在大部分时间里，打包在同一程序集中执行相关函数的例程的功能才有意义，如果这些例程共享相互调用方法的类，则尤为如此。 例如，可以将执行公共语言运行时 (CLR) 触发器和 CLR 存储过程的数据项管理任务的类在同一程序集中打包。 这是因为这些类的方法比起不相关的任务而言更可能调用对方。  
  
 将代码打包到程序集中时，应考虑以下内容：  
  
-   依赖于 CLR 用户定义函数的 CLR 用户定义类型和索引可以导致持久化数据存在于依赖程序集的数据库中。 数据库中具有依赖于程序集的持久化数据时，修改程序集的代码通常更加复杂。 因此，通常将持久化数据相关性依赖（例如使用用户定义函数的用户定义类型和索引）的代码与没有这种持久化数据相关性的代码分开更好。 有关详细信息，请参阅[实现的程序集](../../relational-databases/clr-integration/assemblies-implementing.md)并[ALTER ASSEMBLY &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)。  
  
-   如果托管代码需要更高的权限，最好将该代码与不需要更高权限的代码分开，并将其放入单独的程序集。  
  
## <a name="managing-assembly-security"></a>管理程序集安全性  
 当程序集运行托管代码时，可以控制程序集访问受 .NET 代码访问安全性保护的资源的程度。 执行此操作通过在创建或修改程序集时指定三个权限集之一：安全的 EXTERNAL_ACCESS 或 UNSAFE。  
  
### <a name="safe"></a>SAFE  
 SAFE 是默认的权限集，并且最具限制性。 使用具有 SAFE 权限的程序集运行的代码不能访问外部系统资源（例如文件、网络、环境变量或注册表）。 SAFE 代码可以从本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库访问数据，或执行不涉及访问本地数据库以外资源的计算和业务逻辑。  
  
 大多数程序集执行计算和数据管理任务，而不需要访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外的资源。 因此，建议您将 SAFE 作为程序集权限集。  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS 允许程序集访问某些外部系统资源（例如文件、网络、Web 服务、环境变量和注册表）。 只有具有 EXTERNAL ACCESS 权限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名才能创建 EXTERNAL_ACCESS 程序集。  
  
 SAFE 和 EXTERNAL_ACCESS 程序集只能包含可验证为类型安全的代码。 这意味着这些程序集仅可以通过对类型定义有效的具有定义完善的入口点来访问类。 因此，它们不能随意访问不属于该代码所有的内存缓冲区。 另外，它们不能执行可能对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程的可靠性具有负面影响的操作。  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE 不限制程序集访问资源，包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以内和以外的资源。 在 UNSAFE 程序集内运行的代码可以调用非托管代码。  
  
 同时，指定 UNSAFE 将允许程序集中的代码执行 CLR 验证工具认为是非安全类型的操作。 这些操作可能以非控制的方式访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程空间中的内存缓冲区。 UNSAFE 程序集也可能破坏 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或公共语言运行时的安全系统。 有经验的开发人员或管理员应仅向高度可信的程序集授予 UNSAFE 权限。 只有的成员**sysadmin**固定的服务器角色可以创建 UNSAFE 程序集。  
  
## <a name="restrictions-on-assemblies"></a>对程序集的限制  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对程序集中的托管代码有一些限制，以便确保可以以可靠和可伸缩的方式运行它们。 这意味着在 SAFE 和 EXTERNAL_ACCESS 程序集不允许可能危及服务器可靠性的某些操作。  
  
### <a name="disallowed-custom-attributes"></a>禁止的自定义属性  
 不能用以下自定义属性批注程序集：  
  
```  
System.ContextStaticAttribute  
System.MTAThreadAttribute  
System.Runtime.CompilerServices.MethodImplAttribute  
System.Runtime.CompilerServices.CompilationRelaxationsAttribute  
System.Runtime.Remoting.Contexts.ContextAttribute  
System.Runtime.Remoting.Contexts.SynchronizationAttribute  
System.Runtime.InteropServices.DllImportAttribute   
System.Security.Permissions.CodeAccessSecurityAttribute  
System.STAThreadAttribute  
System.ThreadStaticAttribute  
```  
  
 另外，不能用以下自定义属性批注 SAFE 和 EXTERNAL_ACCESS 程序集：  
  
```  
System.Security.SuppressUnmanagedCodeSecurityAttribute  
System.Security.UnverifiableCodeAttribute  
```  
  
### <a name="disallowed-net-framework-apis"></a>禁止的 .NET Framework API  
 任何[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] API 使用的不允许使用一个批注**Hostprotectionattribute**不能从 SAFE 和 EXTERNAL_ACCESS 程序集调用。  
  
```  
eSelfAffectingProcessMgmt  
eSelfAffectingThreading  
eSynchronization  
eSharedState   
eExternalProcessMgmt  
eExternalThreading  
eSecurityInfrastructure  
eMayLeakOnAbort  
eUI  
```  
  
### <a name="supported-net-framework-assemblies"></a>支持的 .NET Framework 程序集  
 必须使用 CREATE ASSEMBLY 将自定义程序集引用的任何程序集都加载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中。 下列 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 程序集已经加载到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，因此，它们可以由自定义程序集引用，而不必使用 CREATE ASSEMBLY。  
  
```  
custommarshallers.dll  
Microsoft.visualbasic.dll  
Microsoft.visualc.dll  
mscorlib.dll  
system.data.dll  
System.Data.SqlXml.dll  
system.dll  
system.security.dll  
system.web.services.dll  
system.xml.dll  
System.Transactions  
System.Data.OracleClient  
System.Configuration  
```  
  
## <a name="see-also"></a>请参阅  
 [程序集&#40;数据库引擎&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [CLR 集成安全性](../../relational-databases/clr-integration/security/clr-integration-security.md)  
  
  
