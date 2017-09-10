---
title: "nodes （) 方法 (xml 数据类型) |Microsoft 文档"
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
- nodes() method
- nodes method
ms.assetid: 7267fe1b-2e34-4213-8bbf-1c953822446c
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5fbbbd268398ab46b150f647a8d19689d198e6e8
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="nodes-method-xml-data-type"></a>nodes() 方法（xml 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **Nodes （)**方法很有用，当你想要拆分**xml**到关系数据的数据类型实例。 它允许您标识将映射到新行的节点。  
  
 每个**xml**数据类型实例具有隐式提供的上下文节点。 对于在列或变量中存储的 XML 实例来说，它是文档节点。 文档节点是在顶部的隐式节点每个**xml**数据类型实例。  
  
 结果**nodes （)**方法是行集，其中包含原始 XML 实例的逻辑副本。 在这些逻辑副本中，每个行示例的上下文节点都被设置成由查询表达式标识的节点之一。这样，后续的查询可以浏览与这些上下文节点相关的节点。  
  
 您可以从行集中检索多个值。 例如，你可以将应用**value （)**方法返回的行集**nodes （)**并从原始的 XML 实例检索多个值。 请注意， **value （)**方法，当应用于 XML 实例中，仅返回一个值。  
  
## <a name="syntax"></a>语法  
  
```  
  
nodes (XQuery) as Table(Column)  
```  
  
## <a name="arguments"></a>参数  
 *XQuery*  
 字符串文字，即一个 XQuery 表达式。 如果查询表达式构造节点，这些已构造的节点将在结果行集中显示。 如果查询表达式生成一个空序列，则行集将为空。 如果查询表达式静态生成一个包含原子值而不是节点的序列，将产生静态错误。  
  
 *表*(*列*)  
 结果行集的表名称和列名称。  
  
## <a name="remarks"></a>注释  
 例如，假设有下表：  
  
```  
T (ProductModelID int, Instructions xml)  
```  
  
 表中存储了以下生产说明文档。 仅显示一个片段。 注意，文档中有三个生产位置。  
  
```  
<root>  
  <Location LocationID="10"...>  
     <step>...</step>  
     <step>...</step>  
      ...  
  </Location>  
  <Location LocationID="20" ...>  
       ...  
  </Location>  
  <Location LocationID="30" ...>  
       ...  
  </Location>  
</root>  
```  
  
 带有查询表达式 `nodes()` 的 `/root/Location` 方法调用将返回一个行集，其中包含三行（每行都有一个原始 XML 文档的逻辑副本），并且上下文项设置为 `<Location>` 节点之一：  
  
```  
Product  
ModelID      Instructions  
----------------------------------  
1       <root>  
             <Location LocationID="20" ... />  
             <Location LocationID="30" .../></root>  
1      <root><Location LocationID="10" ... />  
  
             <Location LocationID="30" .../></root>  
1      <root><Location LocationID="10" ... />  
             <Location LocationID="20" ... />  
             </root>  
```  
  
 然后可以通过查询此行集**xml**数据类型方法。 以下查询为每个生成的行提取上下文项的子树：  
  
```  
SELECT T2.Loc.query('.')  
FROM   T  
CROSS APPLY Instructions.nodes('/root/Location') as T2(Loc)   
```  
  
 结果如下：  
  
```  
ProductModelID  Instructions  
----------------------------------  
1        <Location LocationID="10" ... />  
1        <Location LocationID="20" ... />  
1        <Location LocationID="30" .../>  
```  
  
 注意，返回的行集已对类型信息进行了维护。 你可以将应用**xml**数据类型方法，如**query （)**， **value （)**， **exist （)**，和**nodes （)**对结果的**nodes （)**方法。 但是，不能将应用**modify （)**方法来修改 XML 实例。  
  
 另外，行集中的上下文节点无法具体化。 即，无法在 SELECT 语句中使用此节点。 但是，可以在 IS NULL 和 COUNT(*) 中使用它。  
  
 使用方案**nodes （)**方法都是与使用相同[OPENXML &#40;Transact SQL &#41;](../../t-sql/functions/openxml-transact-sql.md). 这就提供了 XML 的行集视图。 但是，不需要使用游标，当你使用**nodes （)**包含的 XML 文档的多个行的表上的方法。  
  
 请注意，返回行集**nodes （)**方法是未命名的行集。 因此，必须通过使用别名来显式命名。  
  
 **Nodes （)**函数不能将直接应用到用户定义函数的结果。 若要使用**nodes （)**函数与标量用户定义函数的结果，你可以将用户定义函数的结果赋给变量也可以使用派生的表要分配给该用户定义函数的列别名返回值，然后使用 CROSS APPLY 别名中选择。  
  
 以下示例显示了使用 `CROSS APPLY` 从用户定义函数结果中进行选择的一种方式。  
  
```  
USE AdventureWorks;  
GO  
  
CREATE FUNCTION XTest()  
RETURNS xml  
AS  
BEGIN  
RETURN '<document/>';  
END;  
GO  
  
SELECT A2.B.query('.')  
FROM  
(SELECT dbo.XTest()) AS A1(X)   
CROSS APPLY X.nodes('.') A2(B);  
GO  
  
DROP FUNCTION XTest;  
GO  
```  
  
## <a name="examples"></a>示例  
  
### <a name="using-nodes-method-against-a-variable-of-xml-type"></a>针对 xml 类型的变量使用 nodes() 方法  
 在以下示例中，XML 文档具有一个 <`Root`> 顶级元素和三个 <`row`> 子元素。 查询使用 `nodes()` 方法设置单独的上下文节点，每个 <`row`> 元素一个上下文节点。 `nodes()` 方法返回包含三行的行集。 每行都有一个原始 XML 的逻辑副本，其中每个上下文节点都标识原始文档中的一个不同的 <`row`> 元素。  
  
 然后，查询会从每行返回上下文节点：  
  
```  
DECLARE @x xml   
SET @x='<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>'  
SELECT T.c.query('.') AS result  
FROM   @x.nodes('/Root/row') T(c)  
GO  
```  
  
 结果如下： 在此示例中，查询方法返回上下文项及其内容：  
  
```  
<row id="1"><name>Larry</name><oflw>some text</oflw></row>  
<row id="2"><name>moe</name></row>  
<row id="3"/>  
```  
  
 对上下文节点应用父级取值函数将返回所有三行的 <`Root`> 元素。  
  
```  
SELECT T.c.query('..') AS result  
FROM   @x.nodes('/Root/row') T(c)  
go  
```  
  
 结果如下：  
  
```  
<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>  
<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>  
<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>  
```  
  
### <a name="specifying-the-nodes-method-against-a-column-of-xml-type"></a>针对 xml 类型的列指定 nodes() 方法  
 自行车生产说明此示例中使用和存储中的说明**xml**类型列的**ProductModel**表。  
  
 在下面的示例中，`nodes()`方法指定针对`Instructions`列**xml**键入`ProductModel`表。  
  
 `nodes()` 方法通过指定 `/MI:root/MI:Location` 路径，将 <`Location`> 元素设置为上下文节点。 结果行集包括原始文档的逻辑副本，每个副本对应文档中的一个 <`Location`> 节点，上下文节点设置为 <`Location`> 元素。 因此，`nodes()` 函数提供一组 <`Location`> 上下文节点。  
  
 `query()` 方法对此行集请求 `self::node`，从而在每行中返回 `<Location>` 元素。  
  
 在此示例中，查询在特定产品样式的生产说明文档中将每一个 <`Location`> 元素都设置为上下文节点。 您可以使用这些上下文节点来按照以下方式来检索值：  
  
-   在每个查找位置 Id <`Location`>  
  
-   检索生产步骤 (<`step`> 子元素) 在每个 <`Location`>  
  
 在 `'.'` 方法中，此查询返回上下文项，其中指定了 `self::node()` 的缩写语法 `query()`。  
  
 请注意以下事项：  
  
-   将 `nodes()` 方法应用于 Instructions 列，并且返回行集 `T (C)`。 此行集包含原始生产说明文档的逻辑副本，并且以 `/root/Location` 作为上下文项。  
  
-   CROSS APPLY 将 `nodes()` 应用于 `Instructions` 表中的每行，并且仅返回生成结果集的行。  
  
    ```  
    SELECT C.query('.') as result  
    FROM Production.ProductModel  
    CROSS APPLY Instructions.nodes('  
    declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    /MI:root/MI:Location') as T(C)  
    WHERE ProductModelID=7  
    ```  
  
     下面是部分结果：  
  
    ```  
    <MI:Location LocationID="10"  ...>  
       <MI:step ... />  
          ...  
    </MI:Location>  
    <MI:Location LocationID="20"  ... >  
        <MI:step ... />  
          ...  
    </MI:Location>  
    ...  
    ```  
  
### <a name="applying-nodes-to-the-rowset-returned-by-another-nodes-method"></a>将 nodes() 应用于另一 nodes() 方法返回的行集  
 以下代码查询 XML 文档，以获得 `Instructions` 表的 `ProductModel` 列中的生产说明。 此查询返回包含产品样式 ID、生产位置和生产步骤的行集。  
  
 请注意以下事项：  
  
-   将 `nodes()` 方法应用于 `Instructions` 列，并且返回 `T1 (Locations)` 行集。 此行集包含原始生产说明文档的逻辑副本，并且 `/root/Location` 元素作为项上下文。  
  
-   将 `nodes()` 应用于 `T1 (Locations)` 行集，并且返回 `T2 (steps)` 行集。 此行集包含原始生产说明文档的逻辑副本，并且 `/root/Location/step` 元素作为项上下文。  
  
```  
SELECT ProductModelID, Locations.value('./@LocationID','int') as LocID,  
steps.query('.') as Step         
FROM Production.ProductModel         
CROSS APPLY Instructions.nodes('         
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
/MI:root/MI:Location') as T1(Locations)         
CROSS APPLY T1.Locations.nodes('         
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
./MI:step ') as T2(steps)         
WHERE ProductModelID=7         
GO         
```  
  
 结果如下：  
  
```  
ProductModelID LocID Step         
----------------------------         
7      10   <step ... />         
7      10   <step ... />         
...         
7      20   <step ... />         
7      20   <step ... />         
7      20   <step ... />         
...         
```  
  
 该查询声明 `MI` 前缀两次。 替代方法为，使用 `WITH XMLNAMESPACES` 声明前缀一次，便可将其用于查询：  
  
```  
WITH XMLNAMESPACES (  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions'  AS MI)  
  
SELECT ProductModelID, Locations.value('./@LocationID','int') as LocID,  
steps.query('.') as Step         
FROM Production.ProductModel         
CROSS APPLY Instructions.nodes('         
/MI:root/MI:Location') as T1(Locations)         
CROSS APPLY T1.Locations.nodes('         
./MI:step ') as T2(steps)         
WHERE ProductModelID=7         
GO    
```  
  
## <a name="see-also"></a>另请参阅  
 [使用 WITH XMLNAMESPACES 将命名空间添加到查询](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [创建 XML 数据的实例](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 数据类型方法](../../t-sql/xml/xml-data-type-methods.md)  
  
  

