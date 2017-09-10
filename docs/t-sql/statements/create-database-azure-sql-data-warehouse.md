---
title: "创建数据库 （Azure SQL 数据仓库） |Microsoft 文档"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 03/14/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 42819b93-b757-4b2c-8179-d4be3c512c19
caps.latest.revision: 20
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a178756610f0d0e463c21a2a62a287ada6c863a1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-database-azure-sql-data-warehouse"></a>创建数据库 （Azure SQL 数据仓库）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

创建新数据库。  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for Azure SQL Data Warehouse  
  
CREATE DATABASE database_name [ COLLATE collation_name ]  
(  
    [ MAXSIZE = { 250 | 500 | 750 | 1024 | 5120 | 10240 | 20480 | 30720 | 40960 | 51200 | 61440 | 71680 | 81920 | 92160 | 102400 | 153600 | 204800 | 245760 } GB ,]  
    EDITION = 'datawarehouse',  
    SERVICE_OBJECTIVE = { 'DW100' | 'DW200' | 'DW300' | 'DW400' | 'DW500' | 'DW600' | 'DW1000' | 'DW1200' | 'DW1500' | 'DW2000' | 'DW3000' | 'DW6000' }  
)  
[;]  
```  
  
## <a name="arguments"></a>参数  
*database_name*  
新数据库的名称。 此名称必须是唯一的 SQL server，其中可托管同时[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]数据库和[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]数据库，并应符合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]标识符规则。 有关详细信息，请参阅[标识符](http://go.microsoft.com/fwlink/p/?LinkId=180386)。  
  
*collation_name*  
指定数据库的默认排序规则。 排序规则名称既可以是 Windows 排序规则名称，也可以是 SQL 排序规则名称。 如果未指定，该数据库分配默认排序规则，这是 SQL_Latin1_General_CP1_CI_AS。  
  
有关 Windows 和 SQL 排序规则名称的详细信息，请参阅[COLLATE (TRANSACT-SQL)](http://msdn.microsoft.com/library/ms184391.aspx)。  
  
*版本*  
指定数据库的服务层。 有关[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]使用数据仓库。  
  
*最大大小*  
数据库可能会增长到最大大小。 设置此值禁止除大小组以外的数据库大小的增长。 默认值*MAXSIZE*时未指定为 10240 GB (10 TB)。  其他可能的值范围为 250 GB 达 240 TB。  
  
SERVICE_OBJECTIVE  
指定性能级别。 有关服务目标的详细信息[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，请参阅[SQL 数据仓库上的缩放性能](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-performance-scale/)。  
  
## <a name="general-remarks"></a>一般备注  
使用[DATABASEPROPERTYEX &#40;Transact SQL &#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)若要查看数据库属性。  
  
使用[ALTER DATABASE &#40;Azure SQL 数据仓库 &#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md)若要更改的最大大小，或更高版本服务目标值。   

SQL 数据仓库设置为 COMPATIBILITY_LEVEL 130，并且不能更改。 有关更多详细信息，请参阅[与 Azure SQL 数据库中的兼容性级别 130 改进查询性能](https://azure.microsoft.com/documentation/articles/sql-database-compatibility-level-query-performance-130/)。
  
## <a name="permissions"></a>Permissions  
所需的权限：  
  
-   服务器级别主体登录名，创建由设置过程中，或  
  
-   成员`dbmanager`数据库角色。  
  
## <a name="error-handling"></a>错误处理  
如果数据库的大小达到的 MAXSIZE，你将收到错误代码 40544。 当发生这种情况时，您不能插入和更新数据，或创建新对象 （如表、 存储的过程、 视图和函数）。 你可以仍读取和删除数据、 截断表、 删除表和索引，并重新生成索引。 然后，您可以将 MAXSIZE 更新为比当前数据库大小更大的值，或者删除一些数据以释放存储空间。 在您可以插入新数据之前，可能有长达十五分钟的延迟。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
您必须连接到 master 数据库才能创建新的数据库。  
  
`CREATE DATABASE` 语句必须是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批处理中的唯一语句。

创建数据库后，你无法更改数据库排序规则。   
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]  
  
### <a name="a-simple-example"></a>A. 简单示例  
一个简单的示例，用于创建数据仓库数据库。 这将创建数据库的最小的最大大小，即 10240 GB、 默认排序规则 sql_latin1_general_cp1_ci_as 和的最小的计算能力，这是 DW100。  
  
```  
CREATE DATABASE TestDW  
(EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');  
```  
  
### <a name="b-create-a-data-warehouse-database-with-all-the-options"></a>B. 创建具有所有选项的数据仓库数据库  
创建的示例 10 terabyte 数据仓库使用的所有选项。  
  
```  
CREATE DATABASE TestDW COLLATE Latin1_General_100_CI_AS_KS_WS  
(MAXSIZE = 10240 GB, EDITION = 'datawarehouse', SERVICE_OBJECTIVE = 'DW1000');  
```  
  
## <a name="see-also"></a>另请参阅  
[ALTER DATABASE &#40;Azure SQL 数据仓库 &#40;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md) 
[创建 TABLE &#40;Azure SQL 数据仓库 &#41;](../../t-sql/statements/create-table-azure-sql-data-warehouse.md)  
[删除数据库 &#40;Transact SQL &#40;](../../t-sql/statements/drop-database-transact-sql.md) 
  


