---
title: 传输登录名任务编辑器（"登录" 页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferloginstask.logins.f1
helpviewer_keywords:
- Transfer Logins Task Editor
ms.assetid: bf244c24-bd45-4ece-b66b-78b488f35c5b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ae8ebf56e4ae7c4fce3566cb7688d203b8ceb318
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66054926"
---
# <a name="transfer-logins-task-editor-logins-page"></a>传输登录名任务编辑器（“登录名”页）
  可以使用 **“传输登录名任务编辑器”** 对话框的 **“登录名”** 页，指定用于将一个或多个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 登录名从一个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例复制到另一个实例的属性。 有关此任务的详细信息，请参阅 [Transfer Logins Task](control-flow/transfer-logins-task.md)。  
  
> [!IMPORTANT]  
>  执行传输登录名任务时，在目标服务器上创建的登录名将具有随机的密码，并且密码处于禁用状态。 只有在 **sysadmin** 固定服务器角色的某个成员更改并启用这些登录名的密码后，才可使用这些登录名。 无法传输 **sa** 登录名。  
  
## <a name="options"></a>选项  
 **SourceConnection**  
 在列表中选择一个 SMO 连接管理器，或单击** \<"新建连接 ..." >** 以创建与源服务器的新连接。  
  
 **DestinationConnection**  
 在列表中选择一个 SMO 连接管理器，或单击** \<"新建连接 ..." >** 以创建与目标服务器的新连接。  
  
 **LoginsToTransfer**  
 选择要从源服务器复制到目标服务器的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 登录名。 此属性具有下表所列的选项：  
  
|Value|说明|  
|-----------|-----------------|  
|**AllLogins**|源服务器上的所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 登录名都将复制到目标服务器。|  
|**SelectedLogins**|只有通过 **LoginsList** 指定的登录名才会复制到目标服务器。|  
|**AllLoginsFromSelectedDatabases**|通过 **DatabasesList** 指定的数据库中的所有登录名都将复制到目标服务器。|  
  
 **LoginsList**  
 选择源服务器上要复制到目标服务器的登录名。 只有为 **LoginsToTransfer** 选择了 **SelectedLogins**时，此选项才可用。  
  
 **DatabasesList**  
 选择源服务器上包含要复制到目标服务器的登录名的数据库。 只有为 **LoginsToTransfer** 选择了 **AllLoginsFromSelectedDatabases**时，此选项才可用。  
  
 **IfObjectExists**  
 选择该任务应如何处理目标服务器上已经存在的同名登录名。  
  
 此属性具有下表所列的选项：  
  
|Value|说明|  
|-----------|-----------------|  
|**FailTask**|如果目标服务器上已存在同名的登录名，则任务失败。|  
|**Overwrite**|任务将覆盖目标服务器上同名的登录名。|  
|**略**|任务将跳过目标服务器上存在的同名登录名。|  
  
 **CopySids**  
 选择是否应将与登录名相关联的安全标识符复制到目标服务器。 如果传输登录名任务与传输数据库任务一起使用，则必须将**CopySids** 设置为 **True** 。 否则，传输的数据库将不能识别复制的登录名。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 任务](control-flow/integration-services-tasks.md)   
 [传输登录名任务编辑器 &#40;常规 "页面&#41;](general-page-of-integration-services-designers-options.md)   
 [表达式页](expressions/expressions-page.md)   
 [SMO 连接管理器](connection-manager/smo-connection-manager.md)   
 [强密码](../relational-databases/security/strong-passwords.md)   
 [安装 SQL Server 的安全注意事项](../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
