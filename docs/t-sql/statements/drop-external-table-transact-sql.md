---
title: "删除外部表 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 02a6a236-0756-4570-abfa-6f677a7df042
caps.latest.revision: 12
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 7cf14c5782a5cdc876b04600447892932f9e9921
ms.contentlocale: zh-cn
ms.lasthandoff: 10/24/2017

---
# <a name="drop-external-table-transact-sql"></a>DROP EXTERNAL TABLE (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  删除从 PolyBase 外部表。 这不会删除外部数据。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
DROP EXTERNAL TABLE [ database_name . [schema_name ] . | schema_name . ] table_name   
[;]  
```  
  

## <a name="arguments"></a>参数  
 [ *database_name* 。 [*schema_name*]。 | *schema_name* 。 ] *table_name*  
 若要删除的外部表的一到三部分名称。 架构，或数据库和架构，可以根据需要包含的表名称。  
  
## <a name="permissions"></a>Permissions  
  
-   需要**ALTER**表所属的架构上的权限。  
  
## <a name="general-remarks"></a>一般备注  
 删除外部表中删除所有与表相关的元数据。 它不会删除外部数据。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-basic-syntax"></a>A. 使用基本语法  
  
```  
DROP EXTERNAL TABLE SalesPerson;  
DROP EXTERNAL TABLE dbo.SalesPerson;  
DROP EXTERNAL TABLE EasternDivision.dbo.SalesPerson;  
```  
  
### <a name="b-dropping-an-external-table-from-the-current-database"></a>B. 从当前数据库中删除外部表  
 下面的示例删除`ProductVendor1`表、 其数据、 索引和任何相关的视图，从当前数据库。  
  
```  
DROP EXTERNAL TABLE ProductVendor1;  
```  
  
### <a name="c-dropping-a-table-from-another-database"></a>C. 另一个数据库中删除表  
 以下示例将删除 `EasternDivision` 数据库中的 `SalesPerson` 表。  
  
```  
DROP EXTERNAL TABLE EasternDivision.dbo.SalesPerson;  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE EXTERNAL TABLE (Transact-SQL)](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  


