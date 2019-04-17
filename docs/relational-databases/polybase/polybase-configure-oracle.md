---
title: 配置 PolyBase 以访问 Oracle 中的外部数据 | Microsoft Docs
ms.custom: ''
ms.date: 04/10/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 4a7484acf7a63b5c2a6804e1f3f7914cabaf8524
ms.sourcegitcommit: 57f7e5f25161dbb4cc446e751ea74b1ac5f86165
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2019
ms.locfileid: "59476642"
---
# <a name="configure-polybase-to-access-external-data-in-oracle"></a>配置 PolyBase 以访问 Oracle 中的外部数据

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何使用 SQL Server 实例上的 PolyBase 来查询 Oracle 中的外部数据。

## <a name="prerequisites"></a>必备条件

如果尚未安装 PolyBase，请参阅 [PolyBase 安装](polybase-installation.md)。

## <a name="configure-an-external-table"></a>配置外部表

若要查询 Oracle 数据源中的数据，必须创建外部表以引用外部数据。 本节提供用于创建这些外部表的示例代码。 
 
此部分中使用了以下 Transact-SQL 命令：

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
- [CREATE EXTERNAL TABLE (Transact-SQL)](../../t-sql/statements/create-external-table-transact-sql.md) 
- [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. 创建数据库主密钥（如果尚不存在）。 这是加密凭据密钥所必需的。

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';  
   ```

   > [!NOTE]
   > `PASSWORD` 是用于加密数据库主密钥的密码。 它必须符合托管 SQL Server 实例的计算机的 Windows 密码策略要求。

1. 创建数据库范围的凭据。

   ```sql
   /*  
   * Specify credentials to external data source
   * IDENTITY: user name for external source.  
   * SECRET: password for external source.
   */
   CREATE DATABASE SCOPED CREDENTIAL credential_name
   WITH IDENTITY = 'username', Secret = 'password';
   ```

1. 使用 [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md) 创建外部数据源。 为 Oracle 数据源指定外部数据源位置和凭据。

   ```sql
   /* 
   * LOCATION: Location string should be of format '<vendor>://<server>[:<port>]'.
   * PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
   * CONNECTION_OPTIONS: Specify driver location
   * CREDENTIAL: the database scoped credential, created above.
   */  
   CREATE EXTERNAL DATA SOURCE external_data_source_name
   WITH ( 
     LOCATION = 'oracle://<server address>[:<port>]',
     -- PUSHDOWN = ON | OFF,
     CREDENTIAL = credential_name)
   ```

1. 使用 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 创建外部表，以表示存储在外部 Oracle 系统中的数据。

   ```sql
   /*
   * LOCATION: Oracle table/view in '<database_name>.<schema_name>.<object_name>' format
   * DATA_SOURCE: the external data source, created above.
   */
   CREATE EXTERNAL TABLE customers(
   [O_ORDERKEY] DECIMAL(38) NOT NULL,
   [O_CUSTKEY] DECIMAL(38) NOT NULL,
   [O_ORDERSTATUS] CHAR COLLATE Latin1_General_BIN NOT NULL,
   [O_TOTALPRICE] DECIMAL(15,2) NOT NULL,
   [O_ORDERDATE] DATETIME2(0) NOT NULL,
   [O_ORDERPRIORITY] CHAR(15) COLLATE Latin1_General_BIN NOT NULL,
   [O_CLERK] CHAR(15) COLLATE Latin1_General_BIN NOT NULL,
   [O_SHIPPRIORITY] DECIMAL(38) NOT NULL,
   [O_COMMENT] VARCHAR(79) COLLATE Latin1_General_BIN NOT NULL
   )
   WITH (
    LOCATION='customer',
    DATA_SOURCE=  external_data_source_name
   );
   ```

1. **可选：** 使用以下命令创建外部表的统计信息。

   ```sql
   CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
   ```

   > [!TIP]
   > 建议创建外部表列的统计信息，尤其是用于联接、筛选和聚合的表列。 这会形成最佳查询性能。

## <a name="next-steps"></a>后续步骤

若要了解有关 PolyBase 的详细信息，请参阅 [SQL Server PolyBase 的概述](polybase-guide.md)。
