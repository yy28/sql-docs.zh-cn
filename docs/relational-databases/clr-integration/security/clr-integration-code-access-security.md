---
title: CLR 集成代码访问安全性 |微软文档
description: 对于 SQL Server CLR 集成，CLR 支持托管代码的代码访问安全性，根据代码标识向程序集授予权限。
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
ms.openlocfilehash: 912db3acb6f6dc21952e99da31a1484a9745ed0b
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488300"
---
# <a name="clr-integration-code-access-security"></a>CLR 集成代码访问安全性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  公共语言运行时 (CLR) 支持用于托管代码的一种称为代码访问安全性的安全模式。 在这种模式下，根据代码的标识来对程序集授予权限。 有关详细信息，请参阅 .NET Framework 软件开发包中的“代码访问安全性”部分。  
  
 决定授予程序集的权限的安全策略定义在三个不同的位置：  
  
-   计算机策略：这是对安装了 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的计算机中运行的所有托管代码都有效的策略。  
  
-   用户策略：这是对进程承载的托管代码有效的策略。 对于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，用户策略特定于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务运行时所使用的 Windows 帐户。  
  
-   主机策略：这是由 CLR（在本例中为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]）的主机设置的策略，对该主机中运行的托管代码有效。  
  
 CLR 支持的代码访问安全机制基于如下假设：运行时既可承载完全可信任的代码，也可承载部分可信任的代码。 受 CLR 代码访问安全性保护的资源通常由托管应用程序编程接口包装，这些接口要求提供相应的权限才允许访问资源。 仅当调用堆栈中的所有调用方（在程序集层）均具有相应资源权限时，此权限要求才得到满足。  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中运行时授予托管代码的代码访问安全性权限集为以上三种策略级别授予的权限集的交集。 即使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 向加载到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的程序集授予一个权限集，赋予用户代码的最终权限集仍可能受用户和计算机级别策略的进一步限制。  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>SQL Server 主机策略级别权限集  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 主机策略级别授予程序集的代码访问安全性权限集由创建该程序集时指定的权限集决定。 有三个权限集 **：SAFE、EXTERNAL_ACCESS**和**SAFE（** 使用["创建程序集&#40;交易-SQL&#41;）PERMISSION_SET](../../../t-sql/statements/create-assembly-transact-sql.md)选项指定）。 **EXTERNAL_ACCESS** **PERMISSION_SET**  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 在承载 CLR 的同时向其提供了主机级别安全策略级别；该策略为始终有效的两个策略级别下的附加策略级别。 会为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]创建的每个应用程序域设置此策略。 此策略并不用于在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 创建 CLR 实例时有效的默认应用程序域。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 宿主级别策略组合了用于系统程序集的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固定策略和用于用户程序集的用户指定策略。  
  
 用于 CLR 程序集和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 系统程序集的固定策略授予其完全信任。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 主机策略的用户指定部分基于为每个程序集指定三个权限存储桶之一的程序集所有者。 有关以下列出的安全权限的详细信息，请参阅 .NET Framework SDK。  
  
### <a name="safe"></a>SAFE  
 只允许内部计算和本地数据访问。 **SAFE**是最严格的权限集。 具有**SAFE**权限的程序集执行的代码无法访问外部系统资源，如文件、网络、环境变量或注册表。  
  
 **SAFE**程序集具有以下权限和值：  
  
|权限|值/说明|  
|----------------|-----------------------------|  
|**安全许可**|**执行：** 执行托管代码的权限。|  
|**SqlClientPermission**|**上下文连接 = true，****上下文连接 = 是**：只能使用上下文连接，并且连接字符串只能指定"上下文连接_true"或"上下文连接=是"的值。<br /><br /> **允许空白密码 = 错误：** 不允许使用空白密码。|  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 程序集EXTERNAL_ACCESS具有与**SAFE**程序集相同的权限，具有访问外部系统资源（如文件、网络、环境变量和注册表）的额外能力。  
  
 **EXTERNAL_ACCESS**程序集也具有以下权限和值：  
  
|权限|值/说明|  
|----------------|-----------------------------|  
|**DistributedTransactionPermission**|**无限制：** 允许分布式事务。|  
|**DNSPermission**|**无限制：** 从域名服务器请求信息的权限。|  
|**EnvironmentPermission**|**无限制：** 允许完全访问系统和用户环境变量。|  
|**EventLogPermission**|**管理：** 允许以下操作：创建事件源、读取现有日志、删除事件源或日志、响应条目、清除事件日志、侦听事件以及访问所有事件日志的集合。|  
|**FileIOPermission**|**无限制：** 允许对文件和文件夹的完全访问权限。|  
|**KeyContainerPermission**|**无限制：** 允许完全访问关键容器。|  
|**NetworkInformationPermission**|**访问：** 允许 Pinging。|  
|**RegistryPermission**|允许读取HKEY_CLASSES_ROOT、HKEY_LOCAL_MACHINE、HKEY_CURRENT_USER、HKEY_CURRENT_CONFIG和**HKEY_CURRENT_CONFIG****HKEY_USERS的**读取权。 **HKEY_CLASSES_ROOT** **HKEY_LOCAL_MACHINE** **HKEY_CURRENT_USER**|  
|**安全许可**|**断言：** 能够断言此代码的所有调用方都具有操作的必要权限。<br /><br /> **控制主体：** 能够操作主体对象。<br /><br /> **执行：** 执行托管代码的权限。<br /><br /> **序列化 For物质：** 能够提供序列化服务。|  
|**SmtpPermission**|**访问：** 允许与 SMTP 主机端口 25 的出站连接。|  
|**SocketPermission**|**连接：** 允许传输地址上的出站连接（所有端口、所有协议）。|  
|**SqlClientPermission**|**无限制：** 允许对数据源的完全访问。|  
|**StorePermission**|**无限制：** 允许完全访问 X.509 证书存储。|  
|**WebPermission**|**连接：** 允许与 Web 资源的出站连接。|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE 允许程序集不受限制地访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内部和外部的资源。 在**UNSAFE**程序集中执行的代码也可以调用非托管代码。  
  
 **UNSAFE**程序集被给予**完全信任**。  
  
> [!IMPORTANT]  
>  **SAFE**是执行计算和数据管理任务的程序集的推荐权限设置，而不访问外部[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的资源。 建议**对**访问 外部[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]资源的程序集EXTERNAL_ACCESS。 默认情况下**EXTERNAL_ACCESS**程序集作为[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]服务帐户执行。 **EXTERNAL_ACCESS**代码可以显式模拟调用方的 Windows 身份验证安全上下文。 由于默认值是作为[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]服务帐户执行，因此应仅授予受信任作为服务帐户运行的登录名执行**EXTERNAL_ACCESS**的权限。 从安全角度来看 **，EXTERNAL_ACCESS**和**UNSAFE**程序集是相同的。 但是 **，EXTERNAL_ACCESS**组件提供了不在**UNSAFE**程序集中的各种可靠性和鲁棒性保护。 指定**UNSAFE**允许程序集中的代码对[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]进程空间执行非法操作，因此可能会危及[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的鲁棒性和可伸缩性。 有关在 中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]创建 CLR 程序集的详细信息，请参阅管理[CLR 集成程序集](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)。  
  
## <a name="accessing-external-resources"></a>访问外部资源  
 如果用户定义的类型 （UDT）、存储过程或其他类型的构造程序集注册到**SAFE**权限集，则在构造中执行的托管代码无法访问外部资源。 但是，如果指定**了EXTERNAL_ACCESS**或**UNSAFE**权限集，并且托管代码尝试访问外部资源，请[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]应用以下规则：  
  
|如果|则|  
|--------|----------|  
|执行上下文与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名相对应。|拒绝访问外部资源的尝试并引发一个安全异常。|  
|执行上下文与 Windows 登录名相对应并且执行上下文为原始调用方。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务帐户的安全上下文下访问外部资源。|  
|调用方不是原始调用方。|拒绝访问并引发一个安全异常。|  
|执行上下文与 Windows 登录名相对应并且执行上下文是原始调用方，而该调用方已被模拟。|访问使用调用方安全上下文，而非服务帐户。|  
  
## <a name="permission-set-summary"></a>权限集汇总  
 下图总结了授予**SAFE、EXTERNAL_ACCESS**和**UNSAFE**权限集**EXTERNAL_ACCESS**的限制和权限。  
  
|||||  
|-|-|-|-|  
||**安全**|**EXTERNAL_ACCESS**|**安全**|  
|**代码访问安全权限**|仅执行|执行和访问外部资源|不受限制（包括 P/Invoke）|  
|**编程模型限制**|是|是|无限制|  
|**可验证性要求**|是|是|否|  
|**本地数据访问**|是|是|是|  
|**调用本机代码的能力**|否|否|是|  
  
## <a name="see-also"></a>另请参阅  
 [CLR 集成安全性](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [主机保护属性和 CLR 集成编程](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [CLR 集成编程模型限制](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [CLR 宿主环境](../../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)  
  
  
