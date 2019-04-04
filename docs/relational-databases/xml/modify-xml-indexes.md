---
title: 修改 XML 索引 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XML indexes [SQL Server], modifying
- modifying indexes
ms.assetid: 24d50fe1-c6ec-49e6-91a3-9791851ba53d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1cbd78870aee49d86511a0e4731009374a3b379
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512424"
---
# <a name="modify-xml-indexes"></a>修改 XML 索引
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] DDL 语句可用于修改现有的 XML 和非 XML 索引。 但是，并非所有的 ALTER INDEX 选项都适用于 XML 索引。 修改 XML 索引时以下选项不可用：  
  
-   对于 XML 索引，重新生成和设置选项 IGNORE_DUP_KEY 无效。 对于辅助 XML 索引，重新生成选项 ONLINE 必须设置为 OFF。 在 ALTER INDEX 语句中，不允许 DROP_EXISTING 选项。  
  
-   对用户表中的主键约束进行的修改不会自动传播到 XML 索引中。 用户必须首先删除 XML 索引，然后再重新创建它们。  
  
-   如果指定了 ALTER INDEX ALL，则它将应用于非 XML 索引和 XML 索引。 指定的索引选项可能对两种索引无效。 在这种情况下，整个语句将失败。  
  
## <a name="example-modifying-an-xml-index"></a>例如：修改 XML 索引  
 在以下示例中，创建了 XML 索引，然后通过将选项 `ALLOW_ROW_LOCKS` 设置为 `OFF`来修改该索引。 当 `ALLOW_ROW_LOCKS` 为 `OFF`时，不会锁定行，并且可以使用页级锁和表级锁获得对指定索引的访问权限。  
  
```  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML)  
GO  
-- Create primary XML index.   
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol)  
GO  
-- Note the type 3 is index on XML type.  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T')  
AND name='PIdx_T_XmlCol'  
  
-- Modify and set an index option.  
ALTER INDEX PIdx_T_XmlCol on T   
SET (ALLOW_ROW_LOCKS = OFF)  
```  
  
## <a name="example-disabling-and-enabling-an-xml-index"></a>例如：禁用和启用 XML 索引  
 默认情况下，启用 XML 索引。 如果禁用 XML 索引，则对 XML 列运行的查询不使用 XML 索引。 若要启用 XML 索引，请将 `ALTER INDEX` 和 `REBUILD` 选项一起使用。  
  
```  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML)  
GO  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol ON T(XmlCol)  
GO  
ALTER INDEX PIdx_T_XmlCol on T DISABLE  
Go  
-- Verify index is disabled.  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T')  
AND name='PIdx_T_XmlCol'  
-- Rebuild the index.  
ALTER INDEX PIdx_T_XmlCol on T REBUILD  
Go  
```  
  
## <a name="see-also"></a>另请参阅  
 [XML 索引 (SQL Server)](../../relational-databases/xml/xml-indexes-sql-server.md)  
  
  
