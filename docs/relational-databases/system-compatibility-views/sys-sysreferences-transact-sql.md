---
title: sys.sysreferences (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysreferences
- sys.sysreferences_TSQL
- sysreferences
- sysreferences_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysreferences compatibility view
- sysreferences system table
ms.assetid: 81276f13-202e-4e74-962d-46eb98c98d2e
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 10409e8655925e9ead7c5954332567aded0dc184
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47643456"
---
# <a name="syssysreferences-transact-sql"></a>sys.sysreferences (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  包括 FOREIGN KEY 约束定义到数据库中被引用列的映射。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**constid**|**int**|FOREIGN KEY 约束的 ID。|  
|**fkeyid**|**int**|执行引用表的 ID。|  
|**rkeyid**|**int**|被引用表的 ID。|  
|**rkeyindid**|**smallint**|包含被引用的键列的被引用表的唯一索引的索引 ID。|  
|**keycnt**|**smallint**|键中的列数。|  
|**forkeys**|**varbinary(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**refkeys**|**varbinary(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**fkeydbid**|**smallint**|保留。|  
|**rkeydbid**|**smallint**|保留。|  
|**fkey1**|**smallint**|引用列的列 ID。|  
|**fkey2**|**smallint**|引用列的列 ID。|  
|**fkey3**|**smallint**|引用列的列 ID。|  
|**fkey4**|**smallint**|引用列的列 ID。|  
|**fkey5**|**smallint**|引用列的列 ID。|  
|**fkey6**|**smallint**|引用列的列 ID。|  
|**fkey7**|**smallint**|引用列的列 ID。|  
|**fkey8**|**smallint**|引用列的列 ID。|  
|**fkey9**|**smallint**|引用列的列 ID。|  
|**fkey10**|**smallint**|引用列的列 ID。|  
|**fkey11**|**smallint**|引用列的列 ID。|  
|**fkey12**|**smallint**|引用列的列 ID。|  
|**fkey13**|**smallint**|引用列的列 ID。|  
|**fkey14**|**smallint**|引用列的列 ID。|  
|**fkey15**|**smallint**|引用列的列 ID。|  
|**fkey16**|**smallint**|引用列的列 ID。|  
|**rkey1**|**smallint**|被引用列的列 ID。|  
|**rkey2**|**smallint**|被引用列的列 ID。|  
|**rkey3**|**smallint**|被引用列的列 ID。|  
|**rkey4**|**smallint**|被引用列的列 ID。|  
|**rkey5**|**smallint**|被引用列的列 ID。|  
|**rkey6**|**smallint**|被引用列的列 ID。|  
|**rkey7**|**smallint**|被引用列的列 ID。|  
|**rkey8**|**smallint**|被引用列的列 ID。|  
|**rkey9**|**smallint**|被引用列的列 ID。|  
|**rkey10**|**smallint**|被引用列的列 ID。|  
|**rkey11**|**smallint**|被引用列的列 ID。|  
|**rkey12**|**smallint**|被引用列的列 ID。|  
|**rkey13**|**smallint**|被引用列的列 ID。|  
|**rkey14**|**smallint**|被引用列的列 ID。|  
|**rkey15**|**smallint**|被引用列的列 ID。|  
|**rkey16**|**smallint**|被引用列的列 ID。|  
  
## <a name="see-also"></a>请参阅  
 [系统表映射到系统视图&#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [兼容性视图 (Transact SQL)](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
