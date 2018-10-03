---
title: sys.dm_tran_top_version_generators (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_tran_top_version_generators
- sys.dm_tran_top_version_generators
- dm_tran_top_version_generators_TSQL
- sys.dm_tran_top_version_generators_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_top_version_generators dynamic management view
ms.assetid: cec7809b-ba8a-4df9-b5bb-d4f651ff1a86
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d141da7523501560fc4bd21752ced988c42a7f23
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47755845"
---
# <a name="sysdmtrantopversiongenerators-transact-sql"></a>sys.dm_tran_top_version_generators (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  为生成版本存储区中大多数版本的对象返回一个虚拟表。 **sys.dm_tran_top_version_generators**返回的前 256 聚合记录长度按分组**database_id**并**rowset_id**。 **sys.dm_tran_top_version_generators**通过查询检索数据**dm_tran_version_store**虚拟表。 **sys.dm_tran_top_version_generators**是效率低下视图运行，因为此视图查询版本存储区和版本存储区可能会非常大。 建议使用此函数查找版本存储区的最大使用者。  
  
> [!NOTE]  
>  若要调用此项从[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_tran_top_version_generators**。  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.dm_tran_top_version_generators  
```  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|数据库 ID。|  
|**rowset_id**|**bigint**|行集 ID。|  
|**aggregated_record_length_in_bytes**|**int**|每个记录长度的总和**database_id**并**rowset_id 对**版本存储区中。|  
|**pdw_node_id**|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 对于此分布的节点标识符。|  
  
## <a name="permissions"></a>Permissions

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   

## <a name="remarks"></a>备注  
 因为**sys.dm_tran_top_version_generators**可能必须读取很多页扫描整个版本存储区中，运行**sys.dm_tran_top_version_generators**可能会干扰系统性能。  
  
## <a name="examples"></a>示例  
 下面的示例使用具有四个并发事务的测试方案，每一个事务都由事务序列号 (XSN) 标识，并在 ALLOW_SNAPSHOT_ISOLATION 和 READ_COMMITTED_SNAPSHOT 选项设置为 ON 的数据库中运行。 下列事务正在运行：  
  
-   XSN-57 是序列化隔离下的更新操作。  
  
-   XSN-58 与 XSN-57 相同。  
  
-   XSN-59 是快照隔离下的选择操作。  
  
-   XSN-60 与 XSN-59 相同。  
  
 执行以下查询。  
  
```  
SELECT  
    database_id,  
    rowset_id,  
    aggregated_record_length_in_bytes  
  FROM sys.dm_tran_top_version_generators;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
database_id rowset_id            aggregated_record_length_in_bytes  
----------- -------------------- ---------------------------------  
9           72057594038321152    87  
9           72057594038386688    33  
```  
  
 该输出显示所有版本都创建的`database_id``9`和版本从两个表生成的。  
  
## <a name="see-also"></a>请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与事务相关的动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


