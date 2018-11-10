---
title: 配置 PolyBase 以访问 Teradata 中的外部数据 | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 7abd9873b3aeefb5644ade0497fe89c47d7cd343
ms.sourcegitcommit: 41979c9d511b3eeb45134d30ccb0dbc6bba70f1a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/01/2018
ms.locfileid: "50757952"
---
# <a name="configure-polybase-to-access-external-data-in-teradata"></a>配置 PolyBase 以访问 Teradata 中的外部数据

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何使用 SQL Server 实例上的 PolyBase 来查询 Teradata 中的外部数据。

## <a name="prerequisites"></a>必备条件

如果尚未安装 PolyBase，请参阅 [PolyBase 安装](polybase-installation.md)。 这篇安装文章介绍了安装的先决条件。

若要使用 Teradata 上的 PolyBase，则需要安装 VC++ 可再发行组件。
 
## <a name="configure-an-external-table"></a>配置外部表

若要查询 Teradata 数据源中的数据，必须创建外部表以引用外部数据。 本节提供用于创建这些外部表的示例代码。 

本节中创建了下对象：

- CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)
- CREATE EXTERNAL DATA SOURCE (Transact-SQL) 
- CREATE EXTERNAL TABLE (Transact-SQL) 
- CREATE STATISTICS (Transact-SQL)

1. 创建数据库主密钥（如果尚不存在）。 需要主密钥来加密凭据机密。

     ```sql
      CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';  
     ```
    **参数**

    PASSWORD ='password'

    该密码是否用于加密数据库中的主密钥？ 密码必须符合托管 SQL Server 实例的计算机的 Windows 密码策略要求。

1. 创建数据库范围的凭据。
 
     ```sql
     /*  specify credentials to external data source
      *  IDENTITY: user name for external source.  
     *  SECRET: password for external source.
     */
     CREATE DATABASE SCOPED CREDENTIAL credential_name
     WITH IDENTITY = 'username', Secret = 'password'
     ```

1. 使用 [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md) 创建外部数据源。

     ```sql
    /*  LOCATION: Location string should be of format '<vendor>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    * CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( 
    LOCATION = teradata://<server address>[:<port>],
   -- PUSHDOWN = ON | OFF,
    CREDENTIAL =credential_name
    );

     ```

1.  使用 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 创建表示存储在外部 Teradata 系统中的数据的外部表。
 
     ```sql
     /*  LOCATION: Teradata table/view in '<database_name>.<object_name>' format
      *  DATA_SOURCE: the external data source, created above.
      */
     CREATE EXTERNAL TABLE customer(
      L_ORDERKEY INT NOT NULL,
      L_PARTKEY INT NOT NULL,
     L_SUPPKEY INT NOT NULL,
     L_LINENUMBER INT NOT NULL,
     L_QUANTITY DECIMAL(15,2) NOT NULL,
     L_EXTENDEDPRICE DECIMAL(15,2) NOT NULL,
     L_DISCOUNT DECIMAL(15,2) NOT NULL,
     L_TAX DECIMAL(15,2) NOT NULL,
     L_RETURNFLAG CHAR NOT NULL,
     L_LINESTATUS CHAR NOT NULL,
     L_SHIPDATE DATE NOT NULL,
     L_COMMITDATE DATE NOT NULL,
     L_RECEIPTDATE DATE NOT NULL,
     L_SHIPINSTRUCT CHAR(25) NOT NULL,
     L_SHIPMODE CHAR(10) NOT NULL,
     L_COMMENT VARCHAR(44) NOT NULL
     )
     WITH (
     LOCATION='customer',
     DATA_SOURCE= external_data_source_name
     );
     ```

1. *可选：* 在外部表上创建统计信息。

    为了获得最佳查询性能，请在外部表列上创建统计信息，尤其是用于联接、筛选和聚合的表列。

     ```sql
      CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
     ```

## <a name="next-steps"></a>后续步骤

若要了解有关 PolyBase 的详细信息，请参阅 [SQL Server PolyBase 的概述](polybase-guide.md)。
