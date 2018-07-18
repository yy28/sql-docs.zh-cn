---
title: sys.pdw_loader_run_stages (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 255681e9-323c-42c0-a63c-1f05536efdd5
caps.latest.revision: 8
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5521b046d49fe27c7dd1a174f960caec54e8626e
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37969645"
---
# <a name="syspdwloaderrunstages-transact-sql"></a>sys.pdw_loader_run_stages (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  包含有关中正在进行和已完成加载操作的信息[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。 信息在两次系统重启之间仍会保留。  
  
|||||  
|-|-|-|-|  
|列名|数据类型|Description|范围|  
|run_id|**int**|运行一个加载程序的唯一标识符。||  
|阶段 (stage)|**nvarchar(30)**|运行当前阶段。|CREATE_STAGING、 DMS_LOAD、 LOAD_INSERT、 LOAD_CLEANUP|  
|request_id|**nvarchar(32)**|运行此阶段请求的 ID。||  
|status|**nvarchar(16)**|此阶段的状态。||  
|start_time|**datetime**|该阶段已开始时间。||  
|end_time|**datetime**|阶段结束时间，如果有的话。|如果未启动或正在进行中，则为 NULL。|  
|total_elapsed_time|**int**|运行此阶段所用 （或到目前为止所用） 的总时间。|如果 total_elapsed_time 超过一个整数 （以毫秒为单位的 24.8 天） 的最大值，它将导致具体化失败由于溢出。<br /><br /> 以毫秒为单位的最大值相当于 24.8 天。|  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
