---
title: T-SQL 语句
description: 用于分析平台系统（AP） SQL Server 并行数据仓库（PDW）的 t-sql 语句。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ce80d7a27384f628af02bfa58abcaa351b569d56
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "74399813"
---
# <a name="t-sql-statements-for-parallel-data-warehouse"></a>并行数据仓库的 t-sql 语句
用于分析平台系统（AP） SQL Server 并行数据仓库（PDW）的 transact-sql （T-sql）语句。

## <a name="data-definition-language-ddl-statements"></a>数据定义语言 (DDL) 语句
* [ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw)
* [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md)
* [ALTER PROCEDURE](../t-sql/statements/alter-procedure-transact-sql.md)
* [更改架构](../t-sql/statements/alter-schema-transact-sql.md)
* [ALTER TABLE](../t-sql/statements/alter-table-transact-sql.md)
* [CREATE COLUMNSTORE INDEX](../t-sql/statements/create-columnstore-index-transact-sql.md)
* [CREATE DATABASE](../t-sql/statements/create-database-azure-sql-data-warehouse.md)
* [创建数据库范围的凭据](../t-sql/statements/create-database-scoped-credential-transact-sql.md)
* [CREATE EXTERNAL DATA SOURCE](../t-sql/statements/create-external-data-source-transact-sql.md)
* [CREATE EXTERNAL FILE FORMAT](../t-sql/statements/create-external-file-format-transact-sql.md)
* [创建外部表](../t-sql/statements/create-external-table-transact-sql.md)
* [CREATE FUNCTION](../t-sql/statements/create-function-sql-data-warehouse.md)
* [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md)
* [CREATE PROCEDURE](../t-sql/statements/create-procedure-transact-sql.md)
* [CREATE SCHEMA](../t-sql/statements/create-schema-transact-sql.md)
* [创建统计信息](../t-sql/statements/create-statistics-transact-sql.md)
* [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md)
* [CREATE TABLE 为 SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)
* [CREATE VIEW](../t-sql/statements/create-view-transact-sql.md)
* [删除外部数据源](../t-sql/statements/drop-external-data-source-transact-sql.md)
* [DROP EXTERNAL FILE 格式](../t-sql/statements/drop-external-file-format-transact-sql.md)
* [删除外部表](../t-sql/statements/drop-external-table-transact-sql.md)
* [DROP INDEX](../t-sql/statements/drop-index-transact-sql.md)
* [DROP 过程](../t-sql/statements/drop-procedure-transact-sql.md)
* [删除统计信息](../t-sql/statements/drop-statistics-transact-sql.md)
* [删除表](../t-sql/statements/drop-table-transact-sql.md)
* [删除架构](../t-sql/statements/drop-schema-transact-sql.md)
* [删除视图](../t-sql/statements/drop-view-transact-sql.md)
* [RENAME](../t-sql/statements/rename-transact-sql.md)
* [TRUNCATE TABLE](../t-sql/statements/truncate-table-transact-sql.md)
* [UPDATE STATISTICS](../t-sql/statements/update-statistics-transact-sql.md)

## <a name="data-manipulation-language-dml-statements"></a>数据操作语言 (DML) 语句
* [DELETE](../t-sql/statements/delete-transact-sql.md)
* [INSERT](../t-sql/statements/insert-transact-sql.md)
* [UPDATE](../t-sql/queries/update-transact-sql.md)

## <a name="database-console-commands"></a>数据库控制台命令
* [DBCC DROPCLEANBUFFERS](../t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql.md)
* [DBCC FREEPROCCACHE](https://msdn.microsoft.com/library/mt204018.aspx)
* [DBCC SHRINKLOG](https://msdn.microsoft.com/library/mt204020.aspx)
* [DBCC PDW_SHOWEXECUTIONPLAN](https://msdn.microsoft.com/library/mt204017.aspx)
* [DBCC PDW_SHOWPARTITIONSTATS](https://msdn.microsoft.com/library/mt204013.aspx)
* [DBCC PDW_SHOWSPACEUSED](../t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql.md)
* [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/mt204043.aspx)

## <a name="query-statements"></a>查询语句
* [SELECT](../t-sql/queries/select-transact-sql.md)
* [WITH common_table_expression](../t-sql/queries/with-common-table-expression-transact-sql.md)
* [EXCEPT 和 INTERSECT](../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)
* [EXPLAIN](../t-sql/queries/explain-transact-sql.md)
* [FROM](../t-sql/queries/from-transact-sql.md)
* [使用 PIVOT 和 UNPIVOT](../t-sql/queries/from-using-pivot-and-unpivot.md)
* [分组依据](../t-sql/queries/select-group-by-transact-sql.md)
* [HAVING](../t-sql/queries/select-having-transact-sql.md)
* [ORDER BY](../t-sql/queries/select-order-by-clause-transact-sql.md)
* [选](../t-sql/queries/option-clause-transact-sql.md)
* [交集](../t-sql/language-elements/set-operators-union-transact-sql.md)
* [WHERE](../t-sql/queries/where-transact-sql.md)
* [返回页首](../t-sql/queries/top-transact-sql.md)
* [别名](../t-sql/queries/aliasing-azure-sql-data-warehouse-parallel-data-warehouse.md)
* [搜索条件](../t-sql/queries/search-condition-transact-sql.md)
* [子查询](../t-sql/queries/subqueries-azure-sql-data-warehouse-parallel-data-warehouse.md)

## <a name="security-statements"></a>安全语句
* 权限：[GRANT](../t-sql/statements/grant-transact-sql.md)、[DENY](../t-sql/statements/deny-transact-sql.md)、[REVOKE](../t-sql/statements/revoke-transact-sql.md)
* [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md)
* [更改证书](../t-sql/statements/alter-certificate-transact-sql.md)
* [更改数据库加密密钥](../t-sql/statements/alter-database-encryption-key-transact-sql.md)
* [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)
* [更改主密钥](../t-sql/statements/alter-master-key-transact-sql.md)
* [更改角色](../t-sql/statements/alter-role-transact-sql.md)
* [更改用户](../t-sql/statements/alter-user-transact-sql.md)
* [BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)
* [CLOSE MASTER KEY](../t-sql/statements/close-master-key-transact-sql.md)
* [CREATE CERTIFICATE](../t-sql/statements/create-certificate-transact-sql.md)
* [CREATE DATABASE ENCRYPTION KEY](../t-sql/statements/create-database-encryption-key-transact-sql.md)
* [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)
* [CREATE MASTER KEY](../t-sql/statements/create-master-key-transact-sql.md)
* [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md)
* [创建用户](../t-sql/statements/create-user-transact-sql.md)
* [删除证书](../t-sql/statements/drop-certificate-transact-sql.md)
* [删除数据库加密密钥](../t-sql/statements/drop-database-encryption-key-transact-sql.md)
* [DROP LOGIN](../t-sql/statements/drop-login-transact-sql.md)
* [DROP MASTER KEY](../t-sql/statements/drop-master-key-transact-sql.md)
* [删除角色](../t-sql/statements/drop-role-transact-sql.md)
* [删除用户](../t-sql/statements/drop-user-transact-sql.md)
* [OPEN MASTER KEY](../t-sql/statements/open-master-key-transact-sql.md)

## <a name="next-steps"></a>后续步骤
有关更多参考信息，请参阅[t-sql 语言元素](tsql-language-elements.md)和[t-sql 系统视图](tsql-system-views.md)。

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
