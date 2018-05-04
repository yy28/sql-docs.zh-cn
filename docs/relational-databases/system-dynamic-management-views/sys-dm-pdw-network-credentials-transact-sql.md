---
title: sys.dm_pdw_network_credentials (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.service: ''
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d4fee3ad-6285-4ea5-8513-5e6eb617abb0
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2f3456427ef31af27d6edf64077b2a485c585f01
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmpdwnetworkcredentials-transact-sql"></a>sys.dm_pdw_network_credentials (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  返回的所有网络凭据的列表存储在[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]所有目标服务器的设备。 结果将列出的控件节点和每个计算节点。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|与节点关联的唯一数字 id。|  
|target_server_name|**nvarchar(32)**|目标服务器的 IP 地址，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]将通过使用的用户名和密码凭据访问。|  
|username|**nvarchar(32)**|该密码存储的用户名。|  
|last_modified|**datetime**|修改凭据的最后一个操作的日期时间。|  
  
## <a name="permissions"></a>权限  
 需要 VIEW SERVER STATE。  
  
## <a name="general-remarks"></a>一般备注  
 此动态管理视图的键是*pdw_node_id*加上*target_server_name*。  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
