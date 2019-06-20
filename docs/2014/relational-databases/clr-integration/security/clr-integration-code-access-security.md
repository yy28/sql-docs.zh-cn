---
title: CLR 集成代码访问安全性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- UNSAFE assemblies
- permissions [CLR integration]
- common language runtime [SQL Server], security
- SAFE assemblies
- code access security [CLR integration]
- EXTERNAL_ACCESS assemblies
ms.assetid: 2111cfe0-d5e0-43b1-93c3-e994ac0e9729
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d829ef131bc8772ce2d84391513ffa52b2f2ff1a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62873742"
---
# <a name="clr-integration-code-access-security"></a>CLR 集成代码访问安全性
  公共语言运行时 (CLR) 支持用于托管代码的一种称为代码访问安全性的安全模式。 在这种模式下，根据代码的标识来对程序集授予权限。 有关详细信息，请参阅 .NET Framework 软件开发包中的“代码访问安全性”部分。  
  
 决定授予程序集的权限的安全策略定义在三个不同的位置：  
  
-   计算机策略：这是策略生效的计算机中在其上运行的所有托管代码[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]安装。  
  
-   用户策略：这是对由进程承载的托管代码有效的策略。 有关[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]服务是否正在运行。  
  
-   主机策略：这是由 CLR 主机设置的策略 (在这种情况下， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)])，实际上是该主机中运行的托管代码。  
  
 CLR 支持的代码访问安全机制基于如下假设：运行时既可承载完全可信任的代码，也可承载部分可信任的代码。 由 CLR 代码访问安全性保护的资源通常由包装托管应用程序编程接口该 requirethe 相应的权限才允许访问资源的权限。 仅当所有调用方 （在程序集级别） 的调用堆栈中具有相应的资源权限，则满足 demandfor 权限。  
  
 托管代码的代码访问安全权限授予集内运行时[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]到加载的程序集授予的权限集[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，最终提供给用户代码的权限集可能受限制的更多用户和计算机级别策略。  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>SQL Server 主机策略级别权限集  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 主机策略级别授予程序集的代码访问安全性权限集由创建该程序集时指定的权限集决定。 有三个权限集： `SAFE`，`EXTERNAL_ACCESS`并`UNSAFE`(使用指定**PERMISSION_SET**选项[CREATE ASSEMBLY &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的用户。 此策略并不用于在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 创建 CLR 实例时有效的默认应用程序域。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Fixedpolicy 系统程序集和用户指定策略的用户程序集。  
  
 用于 CLR 程序集和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 系统程序集的固定策略授予其完全信任。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 主机策略的用户指定部分基于为每个程序集指定三个权限存储桶之一的程序集所有者。 有关以下列出的安全权限的详细信息，请参阅 .NET Framework SDK。  
  
### <a name="safe"></a>SAFE  
 允许仅内部计算和本地数据访问。 `SAFE` 是最具限制性的权限集。 由具有 `SAFE` 权限的程序集执行的代码无法访问外部系统资源，例如文件、网络、环境变量或注册表。  
  
 `SAFE` 程序集具有以下权限和值：  
  
|权限|值/说明|  
|----------------|-----------------------------|  
|`SecurityPermission`|`Execution:` 用于执行托管代码的权限。|  
|`SqlClientPermission`|`Context connection = true`、`context connection = yes`：仅可使用上下文连接和连接字符串可以仅指定的值为"上下文连接 = true"或"上下文连接 = yes"。<br /><br /> **AllowBlankPassword = false:** 不允许空白密码。|  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS 程序集具有相同的权限`SAFE`程序集，以及访问外部系统资源，如文件、 网络、 环境变量和注册表的附加功能。  
  
 `EXTERNAL_ACCESS` 程序集还具有以下权限和值：  
  
|权限|值/说明|  
|----------------|-----------------------------|  
|`DistributedTransactionPermission`|`Unrestricted:` 允许分布式的事务。|  
|`DNSPermission`|`Unrestricted:` 若要从域名服务器请求信息的权限。|  
|`EnvironmentPermission`|`Unrestricted:` 允许对系统和用户环境变量进行完全访问。|  
|`EventLogPermission`|`Administer:` 允许执行以下操作：创建事件源、读取现有日志、删除事件源或日志、对项做出响应、清除事件日志、侦听事件以及访问所有事件日志的集合。|  
|`FileIOPermission`|`Unrestricted:` 允许对文件和文件夹进行完全访问。|  
|`KeyContainerPermission`|`Unrestricted:` 允许对密钥容器进行完全访问。|  
|`NetworkInformationPermission`|`Access:` 允许进行 Ping 操作。|  
|`RegistryPermission`|允许对 `HKEY_CLASSES_ROOT`、`HKEY_LOCAL_MACHINE`、`HKEY_CURRENT_USER`、`HKEY_CURRENT_CONFIG` 和 `HKEY_USERS.` 的读取权限。|  
|`SecurityPermission`|`Assertion:` 能够断言此代码的所有调用方都具有执行该操作所需的权限。<br /><br /> `ControlPrincipal:` 能够操作主体对象。<br /><br /> `Execution:` 用于执行托管代码的权限。<br /><br /> `SerializationFormatter:` 能够提供序列化服务。|  
|**SmtpPermission**|`Access:` 允许与 SMTP 主机端口 25 建立出站连接。|  
|`SocketPermission`|`Connect:` 允许与传输地址建立出站连接（所有端口、所有协议）。|  
|`SqlClientPermission`|`Unrestricted:` 允许对数据源进行完全访问。|  
|`StorePermission`|`Unrestricted:` 允许对 X.509 证书存储区进行完全访问。|  
|`WebPermission`|`Connect:` 允许与 Web 资源建立出站连接。|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE 允许程序集不受限制地访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内部和外部的资源。 从 `UNSAFE` 程序集内部执行代码时也可以调用非托管代码。  
  
 `UNSAFE` 程序集被授予 `FullTrust`。  
  
> [!IMPORTANT]  
>  对于执行计算和数据管理任务而无需访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 外部资源的程序集，`SAFE` 是推荐的权限设置。 `EXTERNAL_ACCESS` 默认情况下的程序集执行作为[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]服务帐户、 权限以执行`EXTERNAL_ACCESS`只应该授予作为服务帐户运行的可信登录。 从安全角度来看，`EXTERNAL_ACCESS` 和 `UNSAFE` 程序集是等同的。 但是，`EXTERNAL_ACCESS` 程序集提供了 `UNSAFE` 程序集所不具备的各种可靠性和健壮性保护。 指定`UNSAFE`允许代码程序集中执行非法操作针对[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 有关创建中的 CLR 程序集的详细信息[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，请参阅[管理 CLR 集成程序集](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)。  
  
## <a name="accessing-external-resources"></a>访问外部资源  
 如果用户定义类型 (UDT)、存储过程或其他类型的构造程序集均使用 `SAFE` 权限集进行注册，则在构造中执行的托管代码将无法访问外部资源。 但是，如果指定了 `EXTERNAL_ACCESS` 或 `UNSAFE` 权限集，并且托管代码尝试访问外部资源，则 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 会应用以下规则：  
  
|如果|然后|  
|--------|----------|  
|执行上下文与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名相对应。|拒绝访问外部资源的尝试并引发一个安全异常。|  
|执行上下文与 Windows 登录名相对应并且执行上下文为原始调用方。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务帐户的安全上下文下访问外部资源。|  
|调用方不是原始调用方。|拒绝访问并引发一个安全异常。|  
|执行上下文与 Windows 登录名相对应并且执行上下文是原始调用方，而该调用方已被模拟。|访问使用调用方安全上下文，而非服务帐户。|  
  
## <a name="permission-set-summary"></a>权限集汇总  
 下表总结了授予 `SAFE`、`EXTERNAL_ACCESS` 和 `UNSAFE` 权限集的权限以及为其设定的限制。  
  
|||||  
|-|-|-|-|  
||`SAFE`|`EXTERNAL_ACCESS`|`UNSAFE`|  
|`Code Access Security Permissions`|仅执行|执行和访问外部资源|不受限制（包括 P/Invoke）|  
|`Programming model restrictions`|是|是|无限制|  
|`Verifiability requirement`|是|是|否|  
|`Local data access`|是|是|是|  
|`Ability to call native code`|否|否|是|  
  
## <a name="see-also"></a>请参阅  
 [CLR 集成安全性](clr-integration-security.md)   
 [宿主保护属性和 CLR 集成编程](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [CLR 集成编程模型限制](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [CLR 托管环境](../clr-integration-architecture-clr-hosted-environment.md)  
  
  
