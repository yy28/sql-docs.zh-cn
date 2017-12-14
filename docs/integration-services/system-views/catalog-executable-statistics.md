---
title: catalog.executable_statistics | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 3dda28d6-10d8-4294-9b5e-a6048c07faf9
caps.latest.revision: "7"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: efd64e5612f10b3521849ff2da6103d2975f4830
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="catalogexecutablestatistics"></a>catalog.executable_statistics
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  为运行中的每个可执行文件显示一行，其中包括可执行文件的每次循环迭代。  
  
 可执行文件是添加到包的控制流中的任务或容器。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|Statistics_id|bigint|数据的唯一 ID。|  
|Execution_id|bigint|执行实例的唯一 ID。<br /><br /> Catalog.executions 视图提供了有关执行的其他信息。 有关详细信息，请参阅 [catalog.executions（SSISDB 数据库）](../../integration-services/system-views/catalog-executions-ssisdb-database.md)。|  
|Executable_id|bigint|包组件的唯一 ID。<br /><br /> catalog.executables 视图提供了有关可执行文件的其他信息。 有关详细信息，请参阅 [catalog.executables](../../integration-services/system-views/catalog-executables.md)。|  
|Execution_path|nvarchar(max)|包组件的完整执行路径，包括组件的每次循环迭代。|  
|Start_time|datetimeoffset(7)|可执行文件进入执行前阶段时的时间。|  
|End_time|datetimeoffset(7)|可执行文件进入执行后阶段时的时间。|  
|Execution_duration|int|可执行文件用于执行的时间长度。 该值以毫秒计。|  
|Execution_result|smallint|下面是可能的值：<br /><br /> 0（成功）<br /><br /> 1（失败）<br /><br /> 2（完成）<br /><br /> 3（已取消）|  
|Execution_value|sql_variant|由执行返回的值。 这是用户定义的值。|  
  
## <a name="permissions"></a>Permissions  
 此视图需要下列权限之一：  
  
-   针对执行实例的 READ 权限。  
  
-   ssis_admin 数据库角色的成员资格。  
  
-   sysadmin 服务器角色的成员资格。  
  
  
