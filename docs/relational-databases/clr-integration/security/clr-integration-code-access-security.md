---
title: CLR 集成代码访问安全性 |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
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
ms.openlocfilehash: 25f802f5c9cb67646903179c9100c7014fe466df
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47802275"
---
# <a name="clr-integration-code-access-security"></a>CLR 集成代码访问安全性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  公共语言运行时 (CLR) 支持用于托管代码的一种称为代码访问安全性的安全模式。 在这种模式下，根据代码的标识来对程序集授予权限。 有关详细信息，请参阅 .NET Framework 软件开发包中的“代码访问安全性”部分。  
  
 决定授予程序集的权限的安全策略定义在三个不同的位置：  
  
-   计算机策略：这是对安装了 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的计算机中运行的所有托管代码都有效的策略。  
  
-   用户策略：这是对进程承载的托管代码有效的策略。 对于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，用户策略特定于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务运行时所使用的 Windows 帐户。  
  
-   主机策略：这是由 CLR（在本例中为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]）的主机设置的策略，对该主机中运行的托管代码有效。  
  
 CLR 支持的代码访问安全机制基于如下假设：运行时既可承载完全可信任的代码，也可承载部分可信任的代码。 由 CLR 代码访问安全性保护的资源通常由需要相应的权限才允许访问资源的托管的应用程序编程接口包装。 仅当调用堆栈中的所有调用方（在程序集层）均具有相应资源权限时，此权限要求才得到满足。  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中运行时授予托管代码的代码访问安全性权限集为以上三种策略级别授予的权限集的交集。 即使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 向加载到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的程序集授予一个权限集，赋予用户代码的最终权限集仍可能受用户和计算机级别策略的进一步限制。  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>SQL Server 主机策略级别权限集  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 主机策略级别授予程序集的代码访问安全性权限集由创建该程序集时指定的权限集决定。 有三个权限集：**安全**， **EXTERNAL_ACCESS**并**UNSAFE** (使用指定**PERMISSION_SET** 选项[创建程序集&#40;TRANSACT-SQL&#41;](../../../t-sql/statements/create-assembly-transact-sql.md))。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 在承载 CLR 的同时向其提供了主机级别安全策略级别；该策略为始终有效的两个策略级别下的附加策略级别。 会为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]创建的每个应用程序域设置此策略。 此策略并不用于在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 创建 CLR 实例时有效的默认应用程序域。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 宿主级别策略组合了用于系统程序集的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固定策略和用于用户程序集的用户指定策略。  
  
 用于 CLR 程序集和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 系统程序集的固定策略授予其完全信任。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 主机策略的用户指定部分基于为每个程序集指定三个权限存储桶之一的程序集所有者。 有关以下列出的安全权限的详细信息，请参阅 .NET Framework SDK。  
  
### <a name="safe"></a>SAFE  
 允许仅内部计算和本地数据访问。 **安全**是限制性最强的权限集。 所执行的程序集代码**安全**权限无法访问外部系统资源，例如文件、 网络、 环境变量或注册表。  
  
 **安全**程序集具有以下权限和值：  
  
|权限|值/说明|  
|----------------|-----------------------------|  
|**SecurityPermission**|**执行：** 执行托管的代码的权限。|  
|**SqlClientPermission**|**上下文连接 = true**，**上下文连接 = yes**： 只可以使用上下文连接并且连接字符串可以仅指定的值为"上下文连接 = true"或"上下文连接 = yes"。<br /><br /> **AllowBlankPassword = false:** 不允许使用空白密码。|  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS 程序集具有相同的权限**安全**程序集，以及访问外部系统资源，如文件、 网络、 环境变量和注册表的附加功能。  
  
 **EXTERNAL_ACCESS**程序集还具有以下权限和值：  
  
|权限|值/说明|  
|----------------|-----------------------------|  
|**DistributedTransactionPermission**|**不受限制的：** 允许分布式事务。|  
|**DNSPermission**|**不受限制的：** 从域名服务器请求信息的权限。|  
|**EnvironmentPermission**|**不受限制的：** 完整允许对系统和用户环境变量的访问。|  
|**EventLogPermission**|**管理：** 允许执行以下操作： 创建事件源、 读取现有日志、 删除事件源或日志、 对项，清除事件日志、 侦听事件，并访问的所有事件日志集合做出响应。|  
|**FileIOPermission**|**不受限制的：** 的完全访问权限的文件和文件夹允许。|  
|**KeyContainerPermission**|**不受限制的：** 完整允许密钥容器访问权限。|  
|**NetworkInformationPermission**|**访问：** Pinging 允许。|  
|**RegistryPermission**|允许读取的权**HKEY_CLASSES_ROOT**， **HKEY_LOCAL_MACHINE**， **HKEY_CURRENT_USER**， **HKEY_CURRENT_CONFIG**，和**HKEY_USERS。**|  
|**SecurityPermission**|**断言：** 能够断言此代码的所有调用方均有该操作所需权限。<br /><br /> **ControlPrincipal:** 能够操作主体对象。<br /><br /> **执行：** 执行托管的代码的权限。<br /><br /> **SerializationFormatter:** 能够提供序列化服务。|  
|**SmtpPermission**|**访问：** 允许到 SMTP 主机端口 25 的出站连接。|  
|**SocketPermission**|**连接：** 允许传输地址上的出站连接 （所有端口、 所有协议）。|  
|**SqlClientPermission**|**不受限制的：** 完整允许对数据源进行访问。|  
|**StorePermission**|**不受限制的：** 完全访问存储允许到 X.509 证书。|  
|**WebPermission**|**连接：** 允许对 web 资源的出站连接。|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE 允许程序集不受限制地访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内部和外部的资源。 在执行的代码**UNSAFE**程序集还可以调用非托管的代码。  
  
 **不安全**程序集被授予**FullTrust**。  
  
> [!IMPORTANT]  
>  **安全**是推荐的权限设置的程序集，而无需访问外部资源执行计算和数据管理任务[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 **EXTERNAL_ACCESS**建议用于访问外部资源的程序集[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 **EXTERNAL_ACCESS**作为程序集默认情况下执行[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]服务帐户。 很可能**EXTERNAL_ACCESS**代码显式模拟调用方的 Windows 身份验证安全上下文。 由于默认值是作为执行[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]服务帐户、 权限才能执行**EXTERNAL_ACCESS**只应该授予作为服务帐户运行的可信登录。 从安全角度看**EXTERNAL_ACCESS**并**UNSAFE**程序集完全相同。 但是， **EXTERNAL_ACCESS**程序集提供了可靠性和健壮性保护不在**UNSAFE**程序集。 指定**UNSAFE**允许代码程序集中执行非法操作针对[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]进程空间，并因此可能会损害的可靠性和可伸缩性[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 有关创建中的 CLR 程序集的详细信息[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，请参阅[管理 CLR 集成程序集](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)。  
  
## <a name="accessing-external-resources"></a>访问外部资源  
 如果使用注册的用户定义类型 (UDT)、 存储的过程或其他类型的构造程序集**安全**设置权限，则在构造函数中执行的托管的代码是无法访问外部资源。 但是，如果任一**EXTERNAL_ACCESS**或**UNSAFE**指定权限集，并托管的代码尝试访问外部资源，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]适用以下规则：  
  
|如果|然后|  
|--------|----------|  
|执行上下文与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名相对应。|拒绝访问外部资源的尝试并引发一个安全异常。|  
|执行上下文与 Windows 登录名相对应并且执行上下文为原始调用方。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务帐户的安全上下文下访问外部资源。|  
|调用方不是原始调用方。|拒绝访问并引发一个安全异常。|  
|执行上下文与 Windows 登录名相对应并且执行上下文是原始调用方，而该调用方已被模拟。|访问使用调用方安全上下文，而非服务帐户。|  
  
## <a name="permission-set-summary"></a>权限集汇总  
 下图总结的限制和权限授予**安全**， **EXTERNAL_ACCESS**，并**UNSAFE**权限集。  
  
|||||  
|-|-|-|-|  
||**安全**|**EXTERNAL_ACCESS**|**不安全**|  
|**代码访问安全性权限**|仅执行|执行和访问外部资源|不受限制（包括 P/Invoke）|  
|**编程模型限制**|用户帐户控制|用户帐户控制|无限制|  
|**可验证性要求**|用户帐户控制|是|否|  
|**本地数据访问**|用户帐户控制|是|用户帐户控制|  
|**调用本机代码的能力**|否|否|用户帐户控制|  
  
## <a name="see-also"></a>请参阅  
 [CLR 集成安全性](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [宿主保护属性和 CLR 集成编程](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [CLR 集成编程模型限制](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [CLR 托管环境](../../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)  
  
  
