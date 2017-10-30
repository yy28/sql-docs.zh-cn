---
title: "类型系统 (XQuery) |Microsoft 文档"
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- sequence [XQuery]
- type system [XQuery]
- typed values [XQuery]
- XQuery, sequence
- string values [XQuery]
- XQuery, XPath data type namespace
- xdt prefix [XML in SQL Server]
- XQuery, type system
- built-in XML schema types [SQL Server]
- xs prefix [XML in SQL Server]
ms.assetid: 22d6f861-d058-47ee-b550-cbe9092dcb12
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e84467e5f4ec58e1601868f1406c8c7cfd972a94
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="type-system-xquery"></a>类型系统 (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XQuery 对于架构类型是强类型语言，对于非类型化的数据是弱类型语言。 预定义的 XQuery 类型包括：  
  
-   XML 架构中的内置类型**http://www.w3.org/2001/XMLSchema**命名空间。  
  
-   在中定义的类型**http://www.w3.org/2004/07/xpath-datatypes**命名空间。  
  
 本主题还说明了下列内容：  
  
-   节点的类型化值与字符串值。  
  
-   [数据函数 &#40;XQuery &#41;](../xquery/data-accessor-functions-data-xquery.md)和[字符串函数 &#40;XQuery &#41;](../xquery/data-accessor-functions-string-xquery.md).  
  
-   匹配由表达式返回的序列类型。  
  
## <a name="built-in-types-of-xml-schema"></a>XML 架构的内置类型  
 XML 架构的内置类型具有预定义的命名空间前缀 xs。 这些类型的一些包括**xs:integer**和**xs: string**。 所有这些内置类型都支持。 您可以在创建 XML 架构集合时使用这些类型。  
  
 当查询类型化的 XML 时，节点的静态和动态类型由与正被查询的列或变量相关联的 XML 构架集合确定。 有关静态和动态类型的详细信息，请参阅[表达式上下文和查询计算 &#40;XQuery &#41;](../xquery/expression-context-and-query-evaluation-xquery.md). 例如，指定以下查询对类型化**xml**列 (`Instructions`)。 表达式使用 `instance of` 验证返回的 `LotSize` 属性的类型化值是 `xs:decimal` 类型。  
  
```  
SELECT Instructions.query('  
   DECLARE namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   data(/AWMI:root[1]/AWMI:Location[@LocationID=10][1]/@LotSize)[1] instance of xs:decimal  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 此类型化信息是由与该列关联的 XML 架构集合提供的。  
  
## <a name="types-defined-in-xpath-data-types-namespace"></a>在 XPath 数据类型命名空间中定义的类型  
 中定义的类型**http://www.w3.org/2004/07/xpath-datatypes**命名空间具有预定义的前缀**xdt**。 这些类型的限制条件如下：  
  
-   在创建 XML 架构集合时无法使用这些类型。 这些类型的 XQuery 类型系统中使用，并用于[的 XQuery 和静态类型](../xquery/xquery-and-static-typing.md)。 可以将其转换为原子类型，例如， **xdt:untypedAtomic**中**xdt**命名空间。  
  
-   在查询非类型化的 XML 时，元素节点的静态和动态类型是**xdt： 非类型化**，和属性值的类型是**xdt:untypedAtomic**。 结果**query （)**方法生成非类型化的 XML。 这意味着作为返回，XML 节点**xdt： 非类型化**和**xdt:untypedAtomic**分别。  
  
-   **Xdt:dayTimeDuration**和**xdt:yearMonthDuration**不支持类型。  
  
 在下面的示例中，针对非类型化 XML 变量指定的查询。 表达式 `data(/a[1]`) 返回一个原子值序列。 `data()` 函数返回元素 `<a>` 的类型化值。 由于被查询的 XML 是非类型化的，因此返回值的类型是 `xdt:untypedAtomic`。 因此，`instance of` 将返回 True。  
  
```  
DECLARE @x xml  
SET @x='<a>20</a>'  
SELECT @x.query( 'data(/a[1]) instance of xdt:untypedAtomic' )  
```  
  
 在下面的示例中，表达式 (`/a[1]`) 返回元素 `<a>` 的序列，而不是检索类型化值。 `instance of` 表达式使用元素测试来验证由此表达式返回的值是 `xdt:untyped type` 的元素节点。  
  
```  
DECLARE @x xml  
SET @x='<a>20</a>'  
-- Is this an element node whose name is "a" and type is xdt:untyped.  
SELECT @x.query( '/a[1] instance of element(a, xdt:untyped?)')  
-- Is this an element node of type xdt:untyped.  
SELECT @x.query( '/a[1] instance of element(*, xdt:untyped?)')  
-- Is this an element node?  
SELECT @x.query( '/a[1] instance of element()')  
```  
  
> [!NOTE]  
>  当查询类型化的 XML 实例并且查询表达式包含父轴时，所得到的节点的静态类型信息将不再可用。 但是，动态类型仍然与这些节点关联。  
  
## <a name="typed-value-vs-string-value"></a>类型化值与字符串值  
 每个节点都带有类型化值和字符串值。 对于类型化的 XML 数据，类型化值的类型是与正被查询的列或变量相关联的 XML 架构集合提供的。 对于非类型化的 XML 数据，类型化值的类型是**xdt:untypedAtomic**。  
  
 你可以使用**data （)**或**string （)**函数可检索节点的值：  
  
-   [数据函数 &#40;XQuery &#41;](../xquery/data-accessor-functions-data-xquery.md)返回节点的类型化的值。  
  
-   [字符串函数 &#40;XQuery &#41;](../xquery/data-accessor-functions-string-xquery.md)返回节点的字符串值。  
  
 在下列 XML 架构集合中，定义了整数类型的 <`root`> 元素：  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" type="integer"/>  
</schema>'  
GO  
```  
  
 在下面的示例中，表达式首先检索 `/root[1]` 的类型化值，然后向其添加 `3`。  
  
```  
DECLARE @x xml(SC)  
SET @x='<root>5</root>'  
SELECT @x.query('data(/root[1]) + 3')  
```  
  
 在下一个示例中，表达式将失败，因为表达式中的 `string(/root[1])` 返回字符串类型值。 然后此值将传递给只接受数值类型值作为操作数的算术运算符。  
  
```  
-- Fails because the argument is string type (must be numeric primitive type).  
DECLARE @x xml(SC)  
SET @x='<root>5</root>'  
SELECT @x.query('string(/root[1]) + 3')  
```  
  
 下面的示例计算 `LaborHours` 属性的总计。 `data()`函数检索的类型化的值`LaborHours`中所有属性 <`Location`> 产品型号的元素。 根据与关联的 XML 架构`Instruction`列，`LaborHours`的**xs: decimal**类型。  
  
```  
SELECT Instructions.query('   
DECLARE namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
             sum(data(//AWMI:Location/@LaborHours))   
') AS Result   
FROM Production.ProductModel   
WHERE ProductModelID=7  
```  
  
 此查询将返回结果 12.75。  
  
> [!NOTE]  
>  显式使用**data （)**在此示例中的函数是仅用于说明目的。 如果未指定， **sum （)**隐式应用**data （)**函数提取节点的类型化的值。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Profiler 模板和权限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [XQuery 基础知识](../xquery/xquery-basics.md)  
  
  

