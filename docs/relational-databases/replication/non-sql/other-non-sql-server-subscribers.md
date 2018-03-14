---
title: "其他非 SQL Server 订阅服务器 | Microsoft Docs"
ms.custom: 
ms.date: 03/08/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- non-SQL Server Subscribers, other types
ms.assetid: 96b8beb9-38e8-4ce4-97ca-c0f8656b73b4
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 024860422f6887b335e2e77ba33b3cd0f93c028b
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
# <a name="other-non-sql-server-subscribers"></a>其他非 SQL Server 订阅服务器
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  有关[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持的非 [!INCLUDE[msCoName](../../../includes/msconame-md.md)]订阅服务器列表，请参阅 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)。 本主题包含有关 ODBC 驱动程序和 OLE DB 访问接口要求的信息。  
  
## <a name="odbc-driver-requirements"></a>ODBC 驱动程序要求  
 ODBC 驱动程序：  
  
-   必须符合一级 ODBC (ODBC level-1)。  
  
-   必须是线程安全型分发服务器环境。  
  
-   必须有事务能力。  
  
-   必须支持数据定义语言 (DDL)。  
  
-   不能为只读。  
  
-   必须支持长表名（如 **MSreplication_subscriptions**）。  
  
## <a name="replicating-using-ole-db-interfaces"></a>使用 OLE DB 接口进行复制  
 OLE DB 访问接口必须为事务复制支持下列对象：  
  
-   **DataSource** 对象  
  
-   **Session** 对象  
  
-   **Command** 对象  
  
-   **Rowset** 对象  
  
-   **Error** 对象  
  
### <a name="datasource-object-interfaces"></a>DataSource 对象接口  
 为了连接到数据源，需要下列接口：  
  
-   **IDBInitialize**  
  
-   **IDBCreateSession**  
  
-   **IDBProperties**  
  
 如果访问接口支持 **IDBInfo** 接口，则 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用该接口检索信息（如引用的标识符字符、最大 SQL 语句长度，以及表名和列名中最大字符数）。  
  
### <a name="session-object-interfaces"></a>会话对象接口  
 下列接口是必需的：  
  
-   **IDBCreateCommand**  
  
-   **ITransaction**  
  
-   **ITransactionLocal**  
  
-   **IDBSchemaRowset**  
  
### <a name="command-object-interfaces"></a>Command 对象接口  
 下列接口是必需的：  
  
-   **ICommand**  
  
-   **ICommandProperties**  
  
-   **ICommandText**  
  
-   **ICommandPrepare**  
  
-   **IColumnsInfo**  
  
-   **IAccessor**  
  
-   **ICommandWithParameters**  
  
 **IAccessor** 是创建参数访问器所必需的。 如果访问接口支持 **IColumnRowset**，则 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用该接口确定某列是否为标识列。  
  
### <a name="rowset-object-interfaces"></a>Rowset 对象接口  
 下列接口是必需的：  
  
-   **IRowset**  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
 应用程序应打开在订阅数据库中创建的已复制表上的行集。 访问行集中的数据需要**IColumnsInfo** 和 **IAccessor** 。  
  
### <a name="error-object-interfaces"></a>Error 对象接口  
 下列接口用于管理错误：  
  
-   **IErrorRecords**  
  
-   **IErrorInfo**  
  
 如果 OLE DB 访问接口支持 **ISQLErrorInfo** ，则使用它。  
  
 有关 OLE DB 访问接口的详细信息，请参阅 OLE DB 访问接口附带的文档。  
  
## <a name="see-also"></a>另请参阅  
 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)  
  
  
