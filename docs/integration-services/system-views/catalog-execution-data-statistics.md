---
title: "catalog.execution_data_statistics |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
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
ms.assetid: 6f51407e-0e4e-4b44-af33-db14c9d40ded
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: fa1d87489ff6d0a10d95bf160ded3d038ca39d81
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="catalogexecutiondatastatistics"></a>catalog.execution_data_statistics
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  每当数据流组件向下游组件发送数据时，此视图就会针对给定的包执行显示一行。 此视图中的信息可用于计算组件的数据吞吐量。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|data_stats_id|**bigint**|数据的唯一标识符 (ID)。|  
|execution_id|**bigint**|执行实例的唯一 ID。|  
|package_name|**nvarchar(260)**|在执行过程中启动的第一个包的名称。|  
|task_name|**nvarchar(4000)**|数据流任务的名称。|  
|dataflow_path_id_string|**nvarchar(4000)**|数据流路径的标识字符串。|  
|dataflow_path_name|**nvarchar(4000)**|数据流路径的名称。|  
|source_component_name|**nvarchar(4000)**|发送数据的数据流组件的名称。|  
|destination_component_name|**nvarchar(4000)**|接收数据的数据流组件的名称。|  
|rows_sent|**bigint**|从源组件发送的行数。|  
|created_time|**datatimeoffset(7)**|获取值的时间。|  
|execution_path|**nvarchar(max)**|组件的执行路径。|  
  
## <a name="remarks"></a>注释  
  
-   有来自组件的多个输出时，为每个输出添加一行。  
  
-   默认情况下，开始执行时，不记录有关发送的行数的信息。  
  
-   若要查看此数据用于执行给定的包，请将日志记录级别设置为**详细**。 有关详细信息，请参阅 [Enable Logging for Package Execution on the SSIS Server](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)。  
  
## <a name="permissions"></a>权限  
 此视图需要下列权限之一：  
  
-   针对执行实例的 READ 权限  
  
-   成员资格**ssis_admin**数据库角色  
  
-   成员资格**sysadmin**服务器角色  
  
> [!NOTE]  
>  当您具有在服务器上执行操作的权限时，您还具有查看有关此操作的信息的权限。 将实施行级安全性；只显示您有权查看的行。  
  
  

