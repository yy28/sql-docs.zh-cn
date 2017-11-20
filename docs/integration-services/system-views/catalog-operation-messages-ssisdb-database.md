---
title: "catalog.operation_messages （SSISDB 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- catalog.operation_messages view [Integration Services]
- operation_messages view [Integration Services]
ms.assetid: 0b3cbe38-ce24-47ca-83ef-6538a5299d1a
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 235e9896cbf075bdc26e3df120b23091b8e82d6d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="catalogoperationmessages-ssisdb-database"></a>catalog.operation_messages（SSISDB 数据库）
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中执行操作期间记录的消息。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|operation_message_id|**bigint**|消息的唯一标识符 (ID)。|  
|operation_id|**bigint**|操作的唯一 ID。|  
|message_time|**datetimeoffset(7)**|创建消息时的时间。|  
|message_type|**int**|所显示的消息的类型。|  
|message_source_type|**int**|消息源类型的 ID。|  
|message|**nvarchar(max)**|消息的文本。|  
|extended_info_id|**bigint**|在中找到的其他操作消息中，与相关的信息 ID [extended_operation_info](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md)视图。|  
  
## <a name="remarks"></a>注释  
 此视图对于在目录中执行操作期间记录的每条消息显示一行。 此消息可以由服务器、包执行进程或执行引擎生成。  
  
 此视图显示下列消息类型：  
  
|**message_type**值|Description|  
|-----------------------------|-----------------|  
|-1|Unknown|  
|120|错误|  
|110|警告|  
|70|信息|  
|10|预验证|  
|20|后验证|  
|30|预执行|  
|40|后执行|  
|60|进度|  
|50|StatusChange|  
|100|QueryCancel|  
|130|TaskFailed|  
|90|诊断|  
|200|自定义|  
|140|DiagnosticEx<br /><br /> 每当执行包任务执行子包时，都会记录此事件。 此事件消息包含传递到子包的参数值。<br /><br /> DiagnosticEx 的消息列的值是 XML 文本。|  
|400|NonDiagnostic|  
|80|VariableValueChanged|  
  
 此视图显示下列消息源类型。  
  
|**message_source_type**|Description|  
|-------------------------------|-----------------|  
|10|入口 API，如 T-SQL 和 CLR 存储过程|  
|20|用来运行包的外部进程 (ISServerExec.exe)|  
|30|包级别对象|  
|40|控制流任务|  
|50|控制流容器|  
|60|数据流任务|  
  
## <a name="permissions"></a>Permissions  
 此视图需要下列权限之一：  
  
-   针对操作的 READ 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
> [!NOTE]  
>  当您具有在服务器上执行操作的权限时，您还具有查看有关此操作的信息的权限。 将实施行级安全性；只显示您有权查看的行。  
  
  

