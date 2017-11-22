---
title: "sys.pdw_loader_run_stages (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 255681e9-323c-42c0-a63c-1f05536efdd5
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d209fff76a89f84b67e351864b102ebf8ecbcd5f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwloaderrunstages-transact-sql"></a>sys.pdw_loader_run_stages (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  包含正在进行的和已完成的负载中的操作信息[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。 信息将在系统重新启动后持久保存。  
  
|||||  
|-|-|-|-|  
|列名|数据类型|Description|范围|  
|run_id|**int**|运行加载程序的唯一标识符。||  
|阶段 (stage)|**nvarchar (30)**|运行当前阶段。|CREATE_STAGING、 DMS_LOAD、 LOAD_INSERT、 LOAD_CLEANUP|  
|request_id|**nvarchar(32)**|运行此阶段的请求的 ID。||  
|status|**nvarchar(16)**|此阶段的状态。||  
|start_time|**datetime**|阶段开始时间。||  
|end_time|**datetime**|结束的时间阶段，如果有的话。|如果未启动或正在进行，则为 NULL。|  
|total_elapsed_time|**int**|此阶段所用的 （或到目前为止所用） 的总时间运行。|如果 total_elapsed_time 超过一个整数 （以毫秒为单位的 24.8 天） 的最大值，它将导致具体化失败由于溢出。<br /><br /> 以毫秒为单位的最大值相当于 24.8 天。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
