---
title: "行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], about rowsets
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets
- OLE DB rowsets, about rowsets
- rowsets [OLE DB]
ms.assetid: 5e7b3cbe-3670-4e18-8172-2226e0b6b142
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fe964e8e0cadaee2118540714f6e8a9c43763748
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="rowsets"></a>行集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  行集是一组包含数据列的行。 行集是使所有 OLE DB 数据访问接口能够以表格形式公开结果集数据的中心对象。  
  
 使用者通过创建一个会话后**IDBCreateSession::CreateSession**方法，使用者可以使用两个**IOpenRowset**或**IDBCreateCommand**会话创建行集上的接口。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持这两种接口。 下面描述这两种方法。  
  
-   通过调用创建行集**IOpenRowset::OpenRowset**方法。  
  
     这等同于通过单个表创建行集。 该方法打开并返回行集，其中包括单个基表中的所有行。 自变量之一**OpenRowset**标识从中创建行集的表的表 id。  
  
-   通过调用创建命令对象**IDBCreateCommand::CreateCommand**方法。  
  
     命令对象执行提供程序所支持的命令。 通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口，使用者可以指定任何 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，例如 SELECT 语句或对存储过程的调用。 使用命令对象创建行集的步骤如下：  
  
    1.  使用者调用**IDBCreateCommand::CreateCommand**方法要获取命令对象请求的会话**ICommandText**命令对象上的接口。 这**ICommandText**接口设置和检索实际命令文本。 使用者填入文本命令通过调用**ICommandText::SetCommandText**方法。  
  
    2.  用户调用**ICommand::Execute**命令的方法。 执行命令时生成的行集对象包含该命令产生的结果集。  
  
 使用者可以使用**ICommandProperties**接口，以获取或设置由执行该命令返回的行集的属性**ICommand::Execute**接口。 最经常请求的属性是行集必须支持的接口。 除了接口以外，使用者还可以请求能够修改行集或接口行为的属性。  
  
 使用者释放使用的行集**IRowset::Release**方法。 释放行集时，将释放由该行集的使用者持有的任何行控点。 释放行集时，不会释放取值函数。 如果你有**IAccessor**接口，它仍然存在于正式发行。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [使用 IOpenRowset 创建行集](../../relational-databases/native-client-ole-db-rowsets/creating-a-rowset-with-iopenrowset.md)  
  
-   [使用 ICommand::Execute 创建行集](../../relational-databases/native-client-ole-db-rowsets/creating-rowsets-with-icommand-execute.md)  
  
-   [行集属性和行为](../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
-   [行集和 SQL Server 游标](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md)  
  
-   [提取行](../../relational-databases/native-client-ole-db-rowsets/fetching-rows.md)  
  
-   [提取具有 IRow 的单个行](../../relational-databases/native-client-ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
-   [书签](../../relational-databases/native-client-ole-db-rowsets/bookmarks.md)  
  
-   [更新行集合中的数据](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client (OLE DB)](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
