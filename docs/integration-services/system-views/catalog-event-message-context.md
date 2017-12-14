---
title: catalog.event_message_context | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 273a54f8-b107-4f36-9461-2b475644760d
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb3d3f706bba3e6c0c6cbf88b5c2145e73fdaaeb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="catalogeventmessagecontext"></a>catalog.event_message_context
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  对于 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 服务器上的执行，显示与执行事件消息关联的条件的消息。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|Context_id|bigint|错误上下文的唯一 ID。|  
|Event_message_id|bigint|上下文与之相关的消息的唯一 ID。|  
|Context_depth|int|随着深度的增加，上下文将进一步来自错误。 当错误发生时，上下文深度从 1 开始。 值为 0 指示执行开始前包的状态。|  
|Package_path|Nvarchar(max)|上下文源的包路径。|  
|Context_type|smallint|作为上下文来源的对象的类型。 有关上下文类型的列表，请参阅“备注”部分。|  
|Context_source_name|Nvarchar(4000)|作为上下文来源的对象的名称。|  
|Context_source_id|Nvarchar(38)|作为上下文来源的对象的唯一 ID。|  
|Property_name|Nvarchar(4000)|与上下文的源相关联的属性的名称。|  
|Property_value|Sql_variant|与上下文的源相关联的属性值。|  
  
## <a name="remarks"></a>注释  
 下表列出了上下文类型。  
  
||||  
|-|-|-|  
|上下文类型值|类型名称|Description|  
|10|任务|出错时任务的状态。|  
|20|管道|错误来自管道组件：源、目标或转换组件。|  
|30|序列|序列的状态。|  
|40|For 循环|For 循环的状态。|  
|50|ForEach 循环|Foreach 循环的状态。|  
|60|“包”|出错时包的状态。|  
|70|变量|变量值|  
|80|“ODBC 目标编辑器”|连接管理器的属性。|  
  
## <a name="permissions"></a>Permissions  
 此视图需要下列权限之一：  
  
-   针对操作的 READ 权限  
  
-   ssis_admin 数据库角色的成员资格。  
  
-   sysadmin 服务器角色的成员资格。  
  
  
