---
title: CLR 集成代码访问安全性 |Microsoft Docs
description: 对于 SQL Server CLR 集成，CLR 支持针对托管代码的代码访问安全性，在这种情况下，将根据代码标识向程序集授予权限。
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
ms.openlocfilehash: 1e155e9c6f0e8a85eaf7ec905f9c9b471160a9ec
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85885905"
---
# <a name="clr-integration-code-access-security"></a>CLR 集成代码访问安全性
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  公共语言运行时 (CLR) 支持用于托管代码的一种称为代码访问安全性的安全模式。 在这种模式下，根据代码的标识来对程序集授予权限。 有关详细信息，请参阅 .NET Framework 软件开发包中的“代码访问安全性”部分。  
  
 决定授予程序集的权限的安全策略定义在三个不同的位置：  
  
-   计算机策略：这是对安装了 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的计算机中运行的所有托管代码都有效的策略。  
  
-   用户策略：这是对进程承载的托管代码有效的策略。 对于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，用户策略特定于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务运行时所使用的 Windows 帐户。  
  
-   主机策略：这是由 CLR（在本例中为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]）的主机设置的策略，对该主机中运行的托管代码有效。  
  
 CLR 支持的代码访问安全机制基于如下假设：运行时既可承载完全可信任的代码，也可承载部分可信任的代码。 受 CLR 代码访问安全性保护的资源通常由托管应用程序编程接口包装，这些接口要求提供相应的权限才允许访问资源。 仅当调用堆栈中的所有调用方（在程序集层）均具有相应资源权限时，此权限要求才得到满足。  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中运行时授予托管代码的代码访问安全性权限集为以上三种策略级别授予的权限集的交集。 即使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 向加载到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的程序集授予一个权限集，赋予用户代码的最终权限集仍可能受用户和计算机级别策略的进一步限制。  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>SQL Server 主机策略级别权限集  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 主机策略级别授予程序集的代码访问安全性权限集由创建该程序集时指定的权限集决定。 有三个权限集： **SAFE**、 **EXTERNAL_ACCESS**和**UNSAFE** （使用[CREATE ASSEMBLY &#40;transact-sql&#41;](../../../t-sql/statements/create-assembly-transact-sql.md)的**PERMISSION_SET**选项指定）。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 在承载 CLR 的同时向其提供了主机级别安全策略级别；该策略为始终有效的两个策略级别下的附加策略级别。 会为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]创建的每个应用程序域设置此策略。 此策略并不用于在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 创建 CLR 实例时有效的默认应用程序域。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 宿主级别策略组合了用于系统程序集的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固定策略和用于用户程序集的用户指定策略。  
  
 用于 CLR 程序集和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 系统程序集的固定策略授予其完全信任。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 主机策略的用户指定部分基于为每个程序集指定三个权限存储桶之一的程序集所有者。 有关以下列出的安全权限的详细信息，请参阅 .NET Framework SDK。  
  
### <a name="safe"></a>SAFE  
 只允许内部计算和本地数据访问。 **SAFE**是限制性最强的权限集。 具有**SAFE**权限的程序集执行的代码无法访问外部系统资源，例如文件、网络、环境变量或注册表。  
  
 **安全**程序集具有以下权限和值：  
  
|权限|值/说明|  
|----------------|-----------------------------|  
|**SecurityPermission**|**执行：** 执行托管代码的权限。|  
|**SqlClientPermission**|**上下文连接 = true**，**上下文连接 = 是**：仅可以使用上下文连接，并且连接字符串只能指定 "context connection = true" 或 "context connection = yes" 的值。<br /><br /> **AllowBlankPassword = false：** 不允许使用空白密码。|  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS 程序集具有与**安全**程序集相同的权限，并具有访问外部系统资源（例如文件、网络、环境变量和注册表）的额外功能。  
  
 **EXTERNAL_ACCESS**程序集还具有以下权限和值：  
  
|权限|值/说明|  
|----------------|-----------------------------|  
|**DistributedTransactionPermission**|不**受限：** 允许分布式事务。|  
|**DNSPermission**|不**受限：** 从域名服务器请求信息的权限。|  
|**EnvironmentPermission**|不**受限：** 允许完全访问系统和用户环境变量。|  
|**EventLogPermission**|**管理：** 允许执行以下操作：创建事件源、读取现有的日志、删除事件源或日志、响应条目、清除事件日志、侦听事件和访问所有事件日志的集合。|  
|**FileIOPermission**|不**受限：** 允许完全访问文件和文件夹。|  
|**KeyContainerPermission**|不**受限：** 允许完全访问密钥容器。|  
|**NetworkInformationPermission**|**访问：** 允许 ping。|  
|**RegistryPermission**|允许对**HKEY_CLASSES_ROOT**、 **HKEY_LOCAL_MACHINE**、 **HKEY_CURRENT_USER**、 **HKEY_CURRENT_CONFIG**和 HKEY_USERS 的读取权限 **。**|  
|**SecurityPermission**|**断言：** 能够断言此代码的所有调用方都具有操作的必要权限。<br /><br /> **ControlPrincipal：** 操作主体对象的能力。<br /><br /> **执行：** 执行托管代码的权限。<br /><br /> **SerializationFormatter：** 能够提供序列化服务。|  
|**SmtpPermission**|**访问：** 允许到 SMTP 主机端口25的出站连接。|  
|**SocketPermission**|**连接：** 允许使用传输地址上的出站连接（所有端口、所有协议）。|  
|**SqlClientPermission**|不**受限：** 允许对数据源进行完全访问。|  
|**StorePermission**|不**受限：** 允许完全访问 x.509 证书存储。|  
|**WebPermission**|**连接：** 允许到 web 资源的出站连接。|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE 允许程序集不受限制地访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内部和外部的资源。 从**不安全**程序集内执行的代码还可以调用非托管代码。  
  
 向**不安全**的程序集授予**FullTrust**。  
  
> [!IMPORTANT]  
>  对于执行计算和数据管理任务而无需访问外部资源的程序集，建议使用**SAFE** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 对于访问外部资源的程序集，建议使用**EXTERNAL_ACCESS** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 默认情况下， **EXTERNAL_ACCESS**程序集作为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务帐户执行。 **EXTERNAL_ACCESS**代码可以显式模拟调用方的 Windows 身份验证安全上下文。 由于默认值为作为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务帐户执行，因此，只应将执行**EXTERNAL_ACCESS**的权限提供给受信任的登录名，以便作为服务帐户运行。 从安全角度来看， **EXTERNAL_ACCESS**和**UNSAFE**程序集是相同的。 不过， **EXTERNAL_ACCESS**程序集提供了不同的可靠性和可靠性保护，它们不在不**安全**的程序集中。 指定**UNSAFE**将允许程序集中的代码对进程空间执行非法操作 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，因此可能危及的可靠性和可伸缩性 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 有关在中创建 CLR 程序集的详细信息 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，请参阅[管理 Clr 集成程序集](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)。  
  
## <a name="accessing-external-resources"></a>访问外部资源  
 如果用户定义类型（UDT）、存储过程或其他类型的构造程序集注册到了**SAFE**权限集，则在构造中执行的托管代码将无法访问外部资源。 但是，如果指定了**EXTERNAL_ACCESS**或**UNSAFE**权限集，并且托管代码尝试访问外部资源， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将应用以下规则：  
  
|如果|Then|  
|--------|----------|  
|执行上下文与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名相对应。|拒绝访问外部资源的尝试并引发一个安全异常。|  
|执行上下文与 Windows 登录名相对应并且执行上下文为原始调用方。|在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务帐户的安全上下文下访问外部资源。|  
|调用方不是原始调用方。|拒绝访问并引发一个安全异常。|  
|执行上下文与 Windows 登录名相对应并且执行上下文是原始调用方，而该调用方已被模拟。|访问使用调用方安全上下文，而非服务帐户。|  
  
## <a name="permission-set-summary"></a>权限集汇总  
 下表总结了对**SAFE**、 **EXTERNAL_ACCESS**和**不安全**权限集授予的限制和权限。  
  
|||||  
|-|-|-|-|  
||**防**|**EXTERNAL_ACCESS**|**UNSAFE**|  
|**代码访问安全权限**|仅执行|执行和访问外部资源|不受限制（包括 P/Invoke）|  
|**编程模型限制**|是|是|无限制|  
|**可验证性要求**|是|是|No|  
|**本地数据访问**|是|是|是|  
|**调用本机代码的能力**|否|否|是|  
  
## <a name="see-also"></a>另请参阅  
 [CLR 集成安全性](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [宿主保护属性和 CLR 集成编程](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [CLR 集成编程模型限制](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [CLR 宿主环境](../../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)  
  
  
