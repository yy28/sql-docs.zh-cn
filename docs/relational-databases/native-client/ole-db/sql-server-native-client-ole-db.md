---
title: SQL 服务器本机客户端 （OLE DB） |微软文档
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, about SQL Server Native Client OLE DB provider
- OLE DB, SQL Server Native Client OLE DB provider
- data access [SQL Server Native Client], OLE DB
- SQLNCLI, OLE DB
- OLE DB
- SQL Server Native Client OLE DB provider
- SQL Server Native Client, OLE DB
ms.assetid: da846da4-ec19-4a4f-81fb-7d5a2b2bf80a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 424565f5eb1b0e9ee0770f988090ecb16788c585
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307261"
---
# <a name="sql-server-native-client-ole-db"></a>SQL Server Native Client (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

本机[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序 （SQLNCLI） 是用于访问数据的低级 COM API。 建议将 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口用于开发需要高性能的工具、实用工具或底层组件。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口是直接访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 表格格式数据流 (TDS) 协议的本机高性能访问接口。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 对连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的应用程序提供 OLE DB 支持。  
  
 本机[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序是符合 OLE DB 版本 2.0 的提供程序。  
 
> [!IMPORTANT]
> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库 （SQLNCLI） 仍然被弃用，不建议将其用于新的开发工作。 相反，请使用新的 [Microsoft OLE DB Driver for SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL)，其将使用最新的服务器功能进行更新。
  
## <a name="in-this-section"></a>本节内容  
  
-   [创建 SQL Server Native Client OLE DB 访问接口应用程序](../../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
-   [数据源对象 (OLE DB)](../../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
-   [命令](../../../relational-databases/native-client-ole-db-commands/commands.md)  
  
-   [行集](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
-   [存储过程](../../../relational-databases/native-client/ole-db/stored-procedures.md)  
  
-   [BLOB 和 OLE 对象](../../../relational-databases/native-client-ole-db-blobs/blobs-and-ole-objects.md)  
  
-   [表和索引](../../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
-   [数据类型 (OLE DB)](../../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
-   [架构行集支持 (OLE DB)](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)  
  
-   [表值参数 (OLE DB)](../../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)  
  
-   [日期和时间改进 (OLE DB)](../../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
-   [大型 CLR 用户定义类型 (OLE DB)](../../../relational-databases/native-client/ole-db/large-clr-user-defined-types-ole-db.md)  
  
-   [文件流支持&#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/filestream-support-ole-db.md)  
  
-   [事务](../../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
-   [错误](../../../relational-databases/native-client-ole-db-errors/errors.md)  
  
-   [客户端连接中的服务主体名称 (SPN) (OLE DB)](../../../relational-databases/native-client/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)  
  
-   [稀疏列支持 (OLE DB)](../../../relational-databases/native-client/ole-db/sparse-columns-support-ole-db.md)  
  
-   [SQL 服务器本机客户端&#40;OLE DB&#41; 参考](../../../relational-databases/native-client-ole-db-interfaces/sql-server-native-client-ole-db-interfaces.md)  
  
-   [OLE DB 操作指南主题](../../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 编程](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
