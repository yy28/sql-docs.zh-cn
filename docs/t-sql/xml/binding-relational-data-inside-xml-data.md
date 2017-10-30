---
title: "绑定 XML 数据内的关系数据 |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- relational data binding [SQL Server]
- XML [SQL Server], binding relational data
- xml data type [SQL Server], relational data binding
- binding relational data [XML in SQL Server]
- variables [XML in SQL Server], relational data binding
- columns [XML in SQL Server], relational data binding
ms.assetid: 03d013a9-b53f-46c3-9628-da77f099c74a
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fbb6d199812f90c07e9efa81da11f834e58cdb59
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="binding-relational-data-inside-xml-data"></a>在 XML 数据内部绑定关系数据
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  你可以指定[xml 数据类型方法](../../t-sql/xml/xml-data-type-methods.md)针对**xml**数据类型变量或列。 例如，[查询 &#40; &#41;方法 &#40; xml 数据类型 &#41;](../../t-sql/xml/query-method-xml-data-type.md)执行对 XML 实例的指定的 XQuery。 以这种方式构造 XML 时，您可能想要从一个非 XML 类型列或 Transact-SQL 变量引入一个值。 此过程称为在 XML 内部绑定关系数据。  
  
 若要在 XML 内部绑定非 XML 关系数据，SQL Server 数据库引擎提供了下列伪函数：  
  
-   [sql: column &#40; &#41;函数 &#40;XQuery &#41;](../../xquery/xquery-extension-functions-sql-column.md) ，你可以在 XQuery 或 XML DML 表达式中使用的关系的列中的值。  
  
-   [sql: variable &#40; &#41;函数 &#40;XQuery &#41;](../../xquery/xquery-extension-functions-sql-variable.md) . 允许您在 XQuery 或 XML DML 表达式中使用 SQL 变量的值。  
  
 您可以使用这些函数与**xml**数据类型方法，无论何时你想要公开内 XML 关系的值。  
  
 不能使用这些函数来引用在列或变量中的数据**xml**，CLR 用户定义类型、 datetime、 smalldatetime，**文本**， **ntext**， **sql_variant**，和**映像**类型。  
  
 而且，此绑定用于只读目的。 也就是说，不能在使用这些函数的列中写入数据。 例如，sql:variable("@x") ="*某个表达式"*不允许。  
  
## <a name="example-cross-domain-query-using-sqlvariable"></a>示例：使用 sql:variable() 的跨域查询  
 此示例演示如何**sql: variable**可以使应用程序来参数化查询。 使用 SQL 变量传入 ISBN @isbn。 通过将该常量**sql: variable**，可以使用查询搜索任何 ISBN 和而不仅仅是一个其 ISBN 为 0-7356-1588年-2。  
  
```  
DECLARE @isbn varchar(20)  
SET     @isbn = '0-7356-1588-2'  
SELECT  xCol  
FROM    T  
WHERE   xCol.exist ('/book/@ISBN[. = sql:variable("@isbn")]') = 1  
```  
  
 **sql:column()**可以使用类似的方式并提供其他好处。 可以使用列的索引来提高效率，这由基于开销的查询优化器决定。 另外，计算列可以存储提升的属性。  
  
## <a name="see-also"></a>另请参阅  
 [xml 数据类型方法](../../t-sql/xml/xml-data-type-methods.md)  
  
  

