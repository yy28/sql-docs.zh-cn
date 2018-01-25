---
title: DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: t-sql|database-console-commands
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
caps.latest.revision: "10"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fa9c4e335fddbe4851562f4aada8d55011d99b98
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-pdwshowpartitionstats-transact-sql"></a>DBCC PDW_SHOWPARTITIONSTATS (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

显示的大小和每个分区中的表的行数[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]数据库。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定 &#40;Transact SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
Show the partition stats for a table  
DBCC PDW_SHOWPARTITIONSTATS ( " [ database_name . [ schema_name ] . ] | [ schema_name.] table_name  ")  
[;]  
```  
  
## <a name="arguments"></a>参数  
 [ *database_name* 。 [ *schema_name* ]。 | *schema_name* 。 ] *table_name*  
 一个、 两个，或要显示的表的由三部分名称。  对于两个或三部分的表名称，名称必须用双引号括起来 ("")。 使用一部分表名称周围的引号是可选的。  
  
## <a name="permissions"></a>权限
需要**VIEW SERVER STATE**权限。
  
## <a name="result-sets"></a>结果集  
这是 DBCC PDW_SHOWPARTITIONSTATS 命令的结果。
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|partition_number|int|分区号。|  
|used_page_count|bigint|使用数据的页数。|  
|reserved_page_count|bigint|分配给分区的页面数。|  
|row_count|bigint|在分区中的行数。|  
|pdw_node_id|int|计算节点的数据。|  
|distribution_id|int|分发数据的 id。|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowpartitionstats-basic-syntax-examples"></a>A. DBCC PDW_SHOWPARTITIONSTATS 基本语法示例  
下面的示例显示的已用空间和行数，按分区中的 FactInternetSales 表[!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)]数据库。
  
```sql
DBCC PDW_SHOWPARTITIONSTATS ("ssawPDW.dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS ("dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS (FactInternetSales);  
```  
## <a name="see-also"></a>另请参阅
[DBCC PDW_SHOWEXECUTIONPLAN &#40;Transact-SQL&#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED &#40;Transact-SQL&#41;](dbcc-pdw-showspaceused-transact-sql.md)  
  
