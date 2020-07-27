---
title: 传输登录名任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transferloginstask.f1
- sql13.dts.designer.transferloginstask.general.f1
- sql13.dts.designer.transferloginstask.logins.f1
helpviewer_keywords:
- Transfer Logins task [Integration Services]
ms.assetid: 1df60fd6-c019-405d-8155-c330dbac2cc1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 242a5c58321ad211a7e27b28b4574433c45ceceb
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86914765"
---
# <a name="transfer-logins-task"></a>传输登录名任务

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  传输登录名任务在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例之间传输一个或多个登录名。  
  
## <a name="transfer-logins-between-instances-of-sql-server"></a>在 SQL Server 实例之间传输登录名  
 传输登录名任务支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 源和目标。  
  
## <a name="events"></a>事件  
 该任务将引发报告已传输的登录名数的信息事件，而且在覆盖登录名时还会引发警告事件。  
  
 传输登录名任务并不报告登录名传输的进度，它仅报告 0% 和 100 % 完成。  
  
## <a name="execution-value"></a>执行值  
 在该任务的 **ExecutionValue** 属性中定义的执行值返回已传输的登录名数。 通过将用户定义的变量分配给传输登录名任务的 **ExecValueVariable** 属性，包中的其他对象就可以访问有关登录名传输的信息。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)和[在包中使用变量](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)。  
  
## <a name="log-entries"></a>日志项  
 传输登录名任务包括下列自定义日志项：  
  
-   TransferLoginsTaskStarTransferringObjects   此日志项报告传输已经开始。 日志项包括开始时间。  
  
-   TransferLoginsTaskFinishedTransferringObjects   此日志项报告传输已经完成。 日志项包括结束时间。  
  
 此外，还有 **OnInformation** 事件的日志项（报告已传输的登录名数），以及 **OnWarning** 事件的日志项（是为目标服务器上每个被覆盖的登录名写入的）。  
  
## <a name="security-and-permissions"></a>安全和权限  
 若要浏览源服务器上的登录名并在目标服务器上创建登录名，用户必须同时是这两台服务器上 sysadmin 服务器角色的成员。  
  
## <a name="configuration-of-the-transfer-logins-task"></a>传输登录名任务的配置  
 传输登录名任务可以配置为传输所有登录名，只传输指定登录名，或者只传输对指定的数据库具有访问权限的所有登录名。 无法传输 sa 登录名。 可以重命名 sa 登录名；但是，无法传输重命名的 sa 登录名。  
  
 您还可以指示该任务是否复制与登录名关联的安全标识符 (SID)。 如果传输登录名任务与传输数据库任务结合使用，则必须将 SID 复制到目标数据库，否则目标数据库将无法识别所传输的登录名。  
  
 在目标服务器上，所传输的登录名将被禁用，而且将分配给它们随机的密码。 目标服务器上 sysadmin 角色的成员必须更改这些密码并启用这些登录名，才能使用这些登录名。  
  
 要传输的登录名可能已经存在于目标服务器上。 传输登录名任务可以配置为以下列方式处理现有登录名：  
  
-   覆盖现有登录名。  
  
-   如果存在重复登录名，则该任务失败。  
  
-   跳过重复登录名。  
  
 在运行时，传输登录名任务使用两个 SMO 连接管理器连接到源服务器和目标服务器。 SMO 连接管理器与传输登录名任务分开进行配置，然后在传输登录名任务中引用连接管理器。 SMO 连接管理器指定服务器以及在访问该服务器时要使用的身份验证模式。 有关详细信息，请参阅 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题：  
  
-   [“表达式”页](../../integration-services/expressions/expressions-page.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-logins-task"></a>传输登录名任务的编程配置  
 有关以编程方式设置这些属性的详细信息，请单击以下主题：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferLoginsTask.TransferLoginsTask>  
  
## <a name="transfer-logins-task-editor-general-page"></a>传输登录名任务编辑器（“常规”页）
  可以使用 **“传输登录名任务编辑器”** 对话框的 **“常规”** 页，对传输登录名任务进行命名和说明。  
  
### <a name="options"></a>选项  
 **名称**  
 为传输登录名任务键入唯一的名称。 此名称用作任务图标中的标签。  
  
> [!NOTE]  
>  任务名称在一个包内必须是唯一的。  
  
 **说明**  
 键入传输登录名任务的说明。  
  
## <a name="transfer-logins-task-editor-logins-page"></a>传输登录名任务编辑器（“登录名”页）
  可以使用 **“传输登录名任务编辑器”** 对话框的 **“登录名”** 页，指定用于将一个或多个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名从一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例复制到另一个实例的属性。  
  
> [!IMPORTANT]  
>  执行传输登录名任务时，在目标服务器上创建的登录名将具有随机的密码，并且密码处于禁用状态。 只有在 **sysadmin** 固定服务器角色的某个成员更改并启用这些登录名的密码后，才可使用这些登录名。 无法传输 **sa** 登录名。  
  
### <a name="options"></a>选项  
 **SourceConnection**  
 从列表中选择一个 SMO 连接管理器，或单击“\<New connection...>”以创建到源服务器的新连接。  
  
 **DestinationConnection**  
 从列表中选择一个 SMO 连接管理器，或单击“\<New connection...>”以创建到目标服务器的新连接。  
  
 **LoginsToTransfer**  
 选择要从源服务器复制到目标服务器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 此属性具有下表所列的选项：  
  
|值|说明|  
|-----------|-----------------|  
|**AllLogins**|源服务器上的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名都将复制到目标服务器。|  
|**SelectedLogins**|只有通过 **LoginsList** 指定的登录名才会复制到目标服务器。|  
|**AllLoginsFromSelectedDatabases**|通过 **DatabasesList** 指定的数据库中的所有登录名都将复制到目标服务器。|  
  
 **LoginsList**  
 选择源服务器上要复制到目标服务器的登录名。 只有为 **LoginsToTransfer** 选择了 **SelectedLogins**时，此选项才可用。  
  
 **DatabasesList**  
 选择源服务器上包含要复制到目标服务器的登录名的数据库。 只有为 **LoginsToTransfer** 选择了 **AllLoginsFromSelectedDatabases**时，此选项才可用。  
  
 **IfObjectExists**  
 选择该任务应如何处理目标服务器上已经存在的同名登录名。  
  
 此属性具有下表所列的选项：  
  
|值|说明|  
|-----------|-----------------|  
|**FailTask**|如果目标服务器上已存在同名的登录名，则任务失败。|  
|**Overwrite**|任务将覆盖目标服务器上同名的登录名。|  
|**Skip**|任务将跳过目标服务器上存在的同名登录名。|  
  
 **CopySids**  
 选择是否应将与登录名相关联的安全标识符复制到目标服务器。 如果传输登录名任务与传输数据库任务一起使用，则必须将**CopySids** 设置为 **True** 。 否则，传输的数据库将不能识别复制的登录名。  
  
