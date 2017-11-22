---
title: "sys.pdw_diag_sessions (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
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
ms.assetid: 4d23688a-cddb-4eed-8231-ecde2a0b0e65
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8f9a5a3a19e840c37661b0db95fe5141824e267a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwdiagsessions-transact-sql"></a>sys.pdw_diag_sessions (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  包含有关系统已创建的各种诊断会话的信息。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|**名称**|**nvarchar(255)**|诊断会话的名称。<br /><br /> 此视图的键。||  
|**xml_data**|**nvarchar(4000)**|描述会话的 XML 负载。||  
|**is_active**|**bit**|标志，指示是否处于活动状态的标志。||  
|**host_address**|**nvarchar(255)**|托管的会话定义 （控制节点） 的计算机的地址。||  
|**principal_id**|**int**|在数据库级别创建了会话的用户 ID。||  
|**database_id**|**int**|是诊断会话的作用域的数据库 ID。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
