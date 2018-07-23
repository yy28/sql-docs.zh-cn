---
title: Stretch Database 的限制 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, limitations
- Stretch Database, blocking issues
- limitations (Stretch Database)
- blocking issues (Stretch Database)
ms.assetid: 2b1fbec1-7859-44fc-8417-724fc57a59c0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5537ba71505cf14657e69f0e3ec5ccb8b125ebf3
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38044180"
---
# <a name="limitations-for-stretch-database"></a>Stretch Database 的限制
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  了解有关启用 Stretch 的表的限制，以及当前为表启用 Stretch 的限制。  
  
##  <a name="Caveats"></a> 启用 Stretch 的表的限制  
  
启用 Stretch 的表具有下列限制。  
  
### <a name="constraints"></a>约束  
-   在包含迁移数据的 Azure 表中，UNIQUE 约束和 PRIMARY KEY 约束并未强制唯一性。  
  
### <a name="dml-operations"></a>DML 操作  
-   在启用 Stretch 的表中或包含启用 Stretch 的表的视图中，无法更新或删除已迁移的或符合迁移条件的行。  
  
-   无法在链接服务器上将行插入启用 Stretch 的表。  
  
### <a name="indexes"></a>索引  
-   无法为包含启用 Stretch 的表的视图创建索引。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 索引筛选不会传播至远程表。  
  
##  <a name="Limitations"></a> 当前为表启用 Stretch 的限制  
   
 以下为当前阻止对表启用 Stretch 的项。  
  
 ### <a name="table-properties"></a>表属性  
-   其中超过 1,023 列或超过 998 个索引的表  
  
-   FileTable 或包含 FILESTREAM 数据的表  
  
-   表被复制或正在使用“更改跟踪”或“更改数据捕获”  
  
-   内存优化表  
  
### <a name="data-types"></a>数据类型  
-   ntext、text 和 image  
  
-   TIMESTAMP  
  
-   sql_variant  
  
-   XML  
  
-   CLR 数据类型包括 geometry、geography、hierarchyid 和 CLR 用户定义类型  
  
 ### <a name="column-types"></a>列类型  
 -   COLUMN_SET  
  
-   计算列  
  
### <a name="constraints"></a>约束  
-   默认约束和 CHECK 约束  
  
-   引用表的外键约束 在父子关系（如 Order 和 Order_Detail）中，可以为子表 (Order_Detail) 启用 Stretch，但不能为父表 (Order) 启用 Stretch。  
  
### <a name="indexes"></a>索引  
-   全文检索  
  
-   XML 索引  
  
-   空间索引  
  
-   引用表的索引视图  
  
## <a name="see-also"></a>另请参阅  
 [通过运行 Stretch Database 顾问标识适用于 Stretch Database 的数据库以及表](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)   
 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [为表启用 Stretch Database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
  
