---
title: "OPENXML (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENXML_TSQL
- OPENXML
dev_langs: TSQL
helpviewer_keywords:
- OPENXML statement
- rowsets [SQL Server], XML documents
- XML [SQL Server], rowset views
ms.assetid: 8088b114-7d01-435a-8e0d-b81abacc86d6
caps.latest.revision: "24"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 7b1fb1d28c4bddb679bd4aab8ce6cb11f21caca5
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="openxml-transact-sql"></a>OPENXML (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  OPENXML 通过 XML 文档提供行集视图。 由于 OPENXML 是行集提供程序，因此可在会出现行集提供程序（如表、视图或 OPENROWSET 函数）的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中使用 OPENXML。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
OPENXML( idoc int [ in] , rowpattern nvarchar [ in ] , [ flags byte [ in ] ] )   
[ WITH ( SchemaDeclaration | TableName ) ]  
```  
  
## <a name="arguments"></a>参数  
 *idoc*  
 XML 文档的内部表式形式的文档句柄。 通过调用创建的内部表示形式的 XML 文档**sp_xml_preparedocument**。  
  
 *rowpattern*  
 是用于标识节点的 XPath 模式 (其句柄传递中的 XML 文档中*idoc*参数) 作为行处理。  
  
 *标志*  
 指示应在 XML 数据和关系行集间使用映射以及应如何填充溢出列。 *标志*是可选的输入的参数，并且可以是以下值之一。  
  
|字节值|Description|  
|----------------|-----------------|  
|**0**|默认为**以属性为中心**映射。|  
|**1**|使用**以属性为中心**映射。 可以与 XML_ELEMENTS 一起使用。 在这种情况下，**以属性为中心**首先，应用的映射，然后**以元素为中心**映射应用未得到处理的所有列。|  
|**2**|使用**以元素为中心**映射。 可以与 XML_ATTRIBUTES 一起使用。 在这种情况下，**以属性为中心**首先，应用的映射，然后**以元素为中心**映射应用的所有列未都处理。|  
|**8**|可与 XML_ATTRIBUTES 或 XML_ELEMENTS 组合使用（逻辑或）。 在检索上下文中，此标志指示消耗的数据不应复制到溢出属性 **@mp:xmltext** 。|  
  
 *SchemaDeclaration*  
 是窗体的架构定义： *ColName**ColType* [*ColPattern* | *元属性*] [*ColNameColType* [*ColPattern* | *元属性*]...]  
  
 *ColName*  
 行集中的列名。  
  
 *ColType*  
 行集中列的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型。 如果列类型与不同基础**xml**发生数据类型的属性，类型强制。  
  
 *ColPattern*  
 可选的通用 XPath 模式，它说明应如何将 XML 节点映射到列。 如果*ColPattern*未指定，默认映射 (**以属性为中心**或**以元素为中心**映射，并通过指定的*标志*) 发生。  
  
 为指定的 XPath 模式*ColPattern*用于指定映射的特殊性质 (的情况下**以属性为中心**和**以元素为中心**映射)，覆盖或增强由指定的默认映射*标志*。  
  
 指定为一个常规的 XPath 模式*ColPattern*还支持元属性。  
  
 *元属性*  
 由 OPENXML 提供的元属性之一。 如果*元属性*指定，则该列包含提供的元属性的信息。 使用元属性可以提取有关 XML 节点的信息（如相对位置和命名空间信息）。 它提供了比文本表示形式更详细的信息。  
  
 *表名*  
 是可以提供的表名 (而不是*SchemaDeclaration*) 如果已存在具有所需的架构的表和不所需的任何列模式。  
  
## <a name="remarks"></a>注释  
 WITH 子句提供通过使用行集格式 （和所需的其他映射信息） *SchemaDeclaration*或指定现有*TableName*。 如果未指定可选的 WITH 子句，结果中将返回**边缘**表格式。 边缘表在单个表中表示 XML 文档的细密结构（例如，元素/属性名、文档层次结构、命名空间、处理说明等）。  
  
 下表描述的结构**边缘**表。  
  
|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**id**|**bigint**|文档节点的唯一 ID。<br /><br /> 根元素具有的 ID 值 0。 保留负的 ID 值。|  
|**parentid**|**bigint**|标识节点的父节点。 此 ID 所标识的父节点不一定是父元素，而是取决于此 ID 所标识节点的子节点的 NodeType。 例如，如果节点是文本节点，则其父节点可能是属性节点。<br /><br />  如果节点位于 XML 文档的顶层，则其 ParentID 为 NULL。|  
|**nodetype**|**int**|标识节点类型。 一个对应于 XML DOM 节点类型编号的整数。<br /><br /> 节点类型包括：<br /><br /> 1 = 元素节点<br /><br /> 2 = 属性节点<br /><br /> 3 = 文本节点|  
|**localname**|**nvarchar**|给出元素或属性的本地名称。 如果 DOM 对象没有名称，则为 NULL。|  
|**prefix**|**nvarchar**|节点名称的命名空间前缀。|  
|**namespaceuri**|**nvarchar**|节点的命名空间 URI。 如果值为 NULL，则命名空间不存在。|  
|**datatype**|**nvarchar**|元素或属性行的实际数据类型，否则为 NULL。 数据类型是从内联 DTD 中或从内联架构中推断得出。|  
|**prev**|**bigint**|前一个同级元素的 XML ID。 如果前面没有同级元素，则为 NULL。|  
|**text**|**ntext**|包含属性值或以文本形式的元素内容 (如果为 NULL 或**边缘**表项不需要一个值)。|  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-a-simple-select-statement-with-openxml"></a>A. 使用带 OPENXML 的简单 SELECT 语句  
 以下示例使用 `sp_xml_preparedocument` 创建 XML 图像的内部表示形式。 然后对 XML 文档的内部表示形式执行使用 `SELECT` 行集提供程序的 `OPENXML` 语句。  
  
 *标志*值设置为`1`。 这表示**以属性为中心**映射。 因此，XML 属性映射到行集中的列。 *Rowpattern*指定为`/ROOT/Customer`标识`<Customers>`要处理的节点。  
  
 可选*ColPattern*由于列名称匹配的 XML 属性名称未指定 （列模式） 参数。  
  
 `OPENXML` 行集提供程序创建了一个双列行集（`CustomerID` 和 `ContactName`），`SELECT` 语句从该行集中检索必要的列（在本例中检索所有的列）。  
  
```  
DECLARE @idoc int, @doc varchar(1000);  
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5" OrderDate="1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3" OrderDate="1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>';  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;  
-- Execute a SELECT statement that uses the OPENXML rowset provider.  
SELECT    *  
FROM       OPENXML (@idoc, '/ROOT/Customer',1)  
            WITH (CustomerID  varchar(10),  
                  ContactName varchar(20));  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 如果相同`SELECT`执行语句时使用*标志*设置为`2`，以指示**以元素为中心**的值映射`CustomerID`和`ContactName`为这两个XML 文档中的客户将返回 null 值，因为不存在名为任何元素`CustomerID`或`ContactName`XML 文档中。  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CustomerID ContactName  
---------- -----------  
NULL       NULL  
NULL       NULL  
```  
  
### <a name="b-specifying-colpattern-for-mapping-between-columns-and-the-xml-attributes"></a>B. 为列和 XML 属性之间的映射指定 ColPattern  
 下面的查询从 XML 文档返回客户 ID、订单日期、产品 ID 和数量等属性。 *Rowpattern*标识`<OrderDetails>`元素。 `ProductID` 和 `Quantity` 是 `<OrderDetails>` 元素的属性。 而 `OrderID`、`CustomerID` 和 `OrderDate` 是父元素 (`<Orders>`) 的属性。  
  
 可选*ColPattern*指定。 这包括以下各项：  
  
-   `OrderID`， `CustomerID`，和`OrderDate`于标识的节点的父级的特性的行集映射中*rowpattern* XML 文档中。  
  
-   `ProdID`行集中的列映射到`ProductID`属性，与`Qty`行集中的列映射到`Quantity`中标识节点的属性*rowpattern*。  
  
 尽管**以元素为中心**通过指定映射*标志*参数中指定的映射*ColPattern*覆盖了此映射。  
  
```  
DECLARE @idoc int, @doc varchar(1000);   
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
           OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">v  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
           OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>';   
  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;   
  
-- SELECT stmt using OPENXML rowset provider  
SELECT *  
FROM   OPENXML (@idoc, '/ROOT/Customer/Order/OrderDetail',2)   
         WITH (OrderID       int         '../@OrderID',   
               CustomerID  varchar(10) '../@CustomerID',   
               OrderDate   datetime    '../@OrderDate',   
               ProdID      int         '@ProductID',   
               Qty         int         '@Quantity');  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
OrderID CustomerID           OrderDate                 ProdID    Qty  
------------------------------------------------------------------------  
10248      VINET       1996-07-04 00:00:00.000   11      12  
10248      VINET       1996-07-04 00:00:00.000   42      10  
10283      LILAS       1996-08-16 00:00:00.000   72      3  
```  
  
### <a name="c-obtaining-results-in-an-edge-table-format"></a>C. 获取在边缘表格式的结果  
 以下示例中的示例 XML 文档由 `<Customers>`、`<Orders>` 和 `<Order_0020_Details>` 元素组成。 首先， **sp_xml_preparedocument**调用以获得文档句柄。 此文档句柄传递给 `OPENXML`。  
  
 在`OPENXML`语句， *rowpattern* (`/ROOT/Customers`) 标识`<Customers>`节点来处理。 不带 WITH 子句，因为`OPENXML`返回中的行集**边缘**表格式。  
  
 最后`SELECT`语句检索中的所有列**边缘**表。  
  
```  
DECLARE @idoc int, @doc varchar(1000);   
SET @doc ='  
<ROOT>  
<Customers CustomerID="VINET" ContactName="Paul Henriot">  
   <Orders CustomerID="VINET" EmployeeID="5" OrderDate=  
           "1996-07-04T00:00:00">  
      <Order_x0020_Details OrderID="10248" ProductID="11" Quantity="12"/>  
      <Order_x0020_Details OrderID="10248" ProductID="42" Quantity="10"/>  
   </Orders>  
</Customers>  
<Customers CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Orders CustomerID="LILAS" EmployeeID="3" OrderDate=  
           "1996-08-16T00:00:00">  
      <Order_x0020_Details OrderID="10283" ProductID="72" Quantity="3"/>  
   </Orders>  
</Customers>  
</ROOT>';  
  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;   
  
-- SELECT statement that uses the OPENXML rowset provider.  
SELECT    *  
FROM       OPENXML (@idoc, '/ROOT/Customers')   
EXEC sp_xml_removedocument @idoc;  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [示例：使用 OPENXML](../../relational-databases/xml/examples-using-openxml.md)  
  
  
