---
title: 配置 PolyBase 以使用 ODBC 泛型类型访问外部数据 | Microsoft Docs
ms.custom: ''
ms.date: 10/16/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 3cb5efcb4c4abdc29aa71bf4a5e59ebe039d8a9e
ms.sourcegitcommit: ee76381cfb1c16e0a063315c9c7005f10e98cfe6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2019
ms.locfileid: "55072842"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>配置 PolyBase 以访问 SQL Server 中的外部数据

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

借助 SQL Server 2019 中的 PolyBase，可通过 ODBC 连接器连接到兼容 ODBC 的数据源。 

## <a name="prerequisites"></a>必备条件

请注意，= 功能仅适用于 Windows 上的 SQL Server。 

如果尚未安装 PolyBase，请参阅 [PolyBase 安装](polybase-installation.md)。

首先，在每个 PolyBase 节点上下载并安装要连接的数据源的 ODBC 驱动程序。 正确安装驱动程序后，从“ODBC 数据源管理器”查看和测试该驱动程序。

![PolyBase 横向扩展组](../../relational-databases/polybase/media/polybase-odbc-admin.png) 

> **重要说明！**
> 
> 为提高查询性能，请确保驱动程序已启用连接池。 可通过“ODBC 数据源管理器”完成此操作。
> 
> **注意**
> 
> 在下述步骤 3 中创建外部数据源时，需指定驱动程序的名称（上面圈出的示例）。

## <a name="create-an-external-table"></a>创建外部表

若要查询 ODBC 数据源中的数据，必须创建外部表以引用外部数据。 本节提供用于创建外部表的示例代码。

将在本节中创建以下对象：

- CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL) 
- CREATE EXTERNAL DATA SOURCE (Transact-SQL) 
- CREATE EXTERNAL TABLE (Transact-SQL) 
- CREATE STATISTICS (Transact-SQL)

1. 创建数据库主密钥（如果尚不存在）。 这是加密凭据密钥所必需的。

     ```sql
      CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';  
     ```
    ## <a name="arguments"></a>参数
    PASSWORD ='password'

    用于加密数据库主密钥的密码。 密码必须符合托管 SQL Server 实例的计算机的 Windows 密码策略要求。

1. 创建数据库范围凭据以访问 ODBC 数据源。

     ```sql
     /*  specify credentials to external data source
     *  IDENTITY: user name for external source.  
     *  SECRET: password for external source.
     */
     CREATE DATABASE SCOPED CREDENTIAL credential_name
     WITH IDENTITY = 'username', Secret = 'password';
     ```

1. 使用 [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md) 创建外部数据源。

     ```sql
    /*  LOCATION: Location string should be of format '<type>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( 
    LOCATION = odbc://<ODBC server address>[:<port>],
    CONNECTION_OPTIONS = 'Driver={<Name of Installed Driver>};
    ServerNode = <name of server  address>:<Port>',
    -- PUSHDOWN = ON | OFF,
      CREDENTIAL = credential_name
    );

     ```


1.  使用 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 创建外部表，用以表示外部数据源中的数据。
 
     ```sql
     /*  LOCATION: ODBC data source table/view
     *  DATA_SOURCE: the external data source, created above.
     */
     CREATE EXTERNAL TABLE customer(
     C_CUSTKEY INT NOT NULL,
     C_NAME VARCHAR(25) NOT NULL,
     C_ADDRESS VARCHAR(40) NOT NULL,
     C_NATIONKEY INT NOT NULL,
     C_PHONE CHAR(15) NOT NULL,
     C_ACCTBAL DECIMAL(15,2) NOT NULL,
     C_MKTSEGMENT CHAR(10) NOT NULL,
     C_COMMENT VARCHAR(117) NOT NULL
      )
      WITH (
      LOCATION='customer',
      DATA_SOURCE= external_data_source_name
     );
      ```

1. **可选：** 在外部表上创建统计信息。

    为了获得最佳查询性能，我们建议在外部表列上创建统计信息，尤其是用于联接、筛选和聚合的统计信息。

     ```sql
      CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
     ```

## <a name="next-steps"></a>后续步骤

若要了解有关 PolyBase 的详细信息，请参阅 [SQL Server PolyBase 的概述](polybase-guide.md)。
