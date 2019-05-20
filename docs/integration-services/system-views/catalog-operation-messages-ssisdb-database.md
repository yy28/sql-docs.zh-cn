---
title: catalog.operation_messages（SSISDB 数据库）| Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- catalog.operation_messages view [Integration Services]
- operation_messages view [Integration Services]
ms.assetid: 0b3cbe38-ce24-47ca-83ef-6538a5299d1a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a45ce170d7965ca8358dd6a442a25a67190651cb
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65714385"
---
# <a name="catalogoperationmessages-ssisdb-database"></a>catalog.operation_messages（SSISDB 数据库）

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  显示在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目录中执行操作期间记录的消息。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|operation_message_id|**bigint**|消息的唯一标识符 (ID)。|  
|operation_id|**bigint**|操作的唯一 ID。|  
|message_time|**datetimeoffset(7)**|创建消息时的时间。|  
|message_type|**smallint**|所显示的消息的类型。|  
|message_source_type|**smallint**|消息源类型的 ID。|  
|message|**nvarchar(max)**|消息的文本。|  
|extended_info_id|**bigint**|与在 [extended_operation_info](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md) 视图中找到的操作消息相关的附加信息的 ID。|  
  
## <a name="remarks"></a>Remarks  
 此视图对于在目录中执行操作期间记录的每条消息显示一行。 此消息可以由服务器、包执行进程或执行引擎生成。  
  
 此视图显示下列消息类型：  
  
|**message_type** Value|描述|  
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
  
|**message_source_type**|描述|  
|-------------------------------|-----------------|  
|10|入口 API，如 T-SQL 和 CLR 存储过程|  
|20|用来运行包的外部进程 (ISServerExec.exe)|  
|30|包级别对象|  
|40|控制流任务|  
|50|控制流容器|  
|60|数据流任务|  
  
## <a name="permissions"></a>权限  
 此视图需要下列权限之一：  
  
-   针对操作的 READ 权限  
  
-   **ssis_admin** 数据库角色的成员资格  
  
-   **sysadmin** 服务器角色的成员资格  
  
> [!NOTE]  
>  当您具有在服务器上执行操作的权限时，您还具有查看有关此操作的信息的权限。 将实施行级安全性；只显示您有权查看的行。  
  
  
