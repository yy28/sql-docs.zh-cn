---
title: catalog.executable_statistics | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 3dda28d6-10d8-4294-9b5e-a6048c07faf9
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f170c3a7ba209b7520ae12e193b1a1eccaf62449
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="catalogexecutablestatistics"></a>catalog.executable_statistics
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  为运行中的每个可执行文件显示一行，其中包括可执行文件的每次循环迭代。  
  
 可执行文件是添加到包的控制流中的任务或容器。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|Statistics_id|BIGINT|数据的唯一 ID。|  
|Execution_id|BIGINT|执行实例的唯一 ID。<br /><br /> Catalog.executions 视图提供了有关执行的其他信息。 有关详细信息，请参阅 [catalog.executions（SSISDB 数据库）](../../integration-services/system-views/catalog-executions-ssisdb-database.md)。|  
|Executable_id|BIGINT|包组件的唯一 ID。<br /><br /> catalog.executables 视图提供了有关可执行文件的其他信息。 有关详细信息，请参阅 [catalog.executables](../../integration-services/system-views/catalog-executables.md)。|  
|Execution_path|nvarchar(max)|包组件的完整执行路径，包括组件的每次循环迭代。|  
|Start_time|datetimeoffset(7)|可执行文件进入执行前阶段时的时间。|  
|End_time|datetimeoffset(7)|可执行文件进入执行后阶段时的时间。|  
|Execution_duration|ssNoversion|可执行文件用于执行的时间长度。 该值以毫秒计。|  
|Execution_result|SMALLINT|下面是可能的值：<br /><br /> 0（成功）<br /><br /> 1（失败）<br /><br /> 2（完成）<br /><br /> 3（已取消）|  
|Execution_value|sql_variant|由执行返回的值。 这是用户定义的值。|  
  
## <a name="permissions"></a>权限  
 此视图需要下列权限之一：  
  
-   针对执行实例的 READ 权限。  
  
-   **ssis_admin** 数据库角色的成员资格。  
  
-   **sysadmin** 服务器角色的成员资格。  
  
  
