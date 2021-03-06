---
description: catalog.execution_data_statistics
title: catalog.execution_data_statistics | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 6f51407e-0e4e-4b44-af33-db14c9d40ded
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 24452ceffc1660e57b087395ded3923e47802314
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495213"
---
# <a name="catalogexecution_data_statistics"></a>catalog.execution_data_statistics 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  每当数据流组件向下游组件发送数据时，此视图就会针对给定的包执行显示一行。 此视图中的信息可用于计算组件的数据吞吐量。  
  
|列名称|数据类型|说明|  
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
  
## <a name="remarks"></a>备注  
  
-   有来自组件的多个输出时，为每个输出添加一行。  
  
-   默认情况下，开始执行时，不记录有关发送的行数的信息。  
  
-   要查看给定包执行的这些数据，请将日志记录级别设置为“详细”****。 有关详细信息，请参阅 [在 SSIS 服务器上启用包执行的日志记录](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)。  
  
## <a name="permissions"></a>权限  
 此视图需要下列权限之一：  
  
-   针对执行实例的 READ 权限  
  
-   **ssis_admin** 数据库角色的成员资格  
  
-   **sysadmin** 服务器角色的成员资格  
  
> [!NOTE]  
>  当您具有在服务器上执行操作的权限时，您还具有查看有关此操作的信息的权限。 将实施行级安全性；只显示您有权查看的行。  
  
  
