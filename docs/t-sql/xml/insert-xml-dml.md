---
title: "插入 (XML DML) |Microsoft 文档"
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
- XML DML [SQL Server]
- inserting nodes
- insert keyword [XML DML]
- insert XML DML statement
ms.assetid: 0c95c2b3-5cc2-4c38-9e25-86493096c442
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9f995a0dcd0b91c0835c4121a7a2072c2a586f35
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="insert-xml-dml"></a>插入 (XML DML)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  将插入一个或多个节点由标识*Expression1*作为子节点或由标识的节点的同级*Expression2*。  
  
## <a name="syntax"></a>语法  
  
```  
  
insert   
      Expression1 (  
                 {as first | as last} into | after | before  
                                    Expression2  
                )  
```  
  
## <a name="arguments"></a>参数  
 *Expression1*  
 标识要插入的一个或多个节点。 这可以是常量的 XML 实例;对在其应用修改方法; 的同一个 XML 架构集合的类型化 XML 数据类型实例的引用使用独立的非类型化的 XML 数据类型实例**sql:column()**/**sql: variable**函数; 或 XQuery 表达式。 该表达式可以得出节点、文本节点或一组有序的节点。 但它无法解得根 (/) 节点。 如果该表达式得出一个值或一组值，则这些值作为单个文本节点插入，各值之间以空格分隔开。 如果将多个节点指定为常量，则这些节点用括号括住，并以逗号分隔开。 但无法插入异构序列（如一组元素、属性或值）。 如果*Expression1*解析为空序列，没有插入发生，并且不会返回错误。  
  
 into  
 通过标识节点*Expression1*作为直接子文件夹 （子节点） 由标识的节点插入*Expression2*。 如果中的节点*Expression2*已有一个或多个子节点，你必须采用两种**为第一个**或**最后**以指定要添加的新节点。 例如，分别在子列表的开头或末尾。 **为第一个**和**最后**关键字时插入属性被忽略。  
  
 after  
 通过标识节点*Expression1*由标识节点的后面插入成为直接同级*Expression2*。 **后**关键字不能用于插入属性。 例如，它不能用于插入属性构造函数或从 XQuery 返回属性。  
  
 before  
 通过标识节点*Expression1*作为同级直接由标识的节点插入*Expression2*。 **之前**正在插入属性时，不能使用关键字。 例如，它不能用于插入属性构造函数或从 XQuery 返回属性。  
  
 *Expression2*  
 标识节点。 标识节点*Expression1*相对于由标识节点插入*Expression2*。 这可以是 XQuery 表达式，返回当前被引用的文档中现有节点的引用。 如果返回多个节点，则插入失败。 如果*Expression2*返回发生空序列，任何插入操作将返回并没有错误。 如果*Expression2*静态不是单一实例，返回一个静态的错误。 *Expression2*不能为处理指令、 注释或属性。 请注意， *Expression2*必须是对文档中的现有节点并不是构造的节点的引用。  
  
## <a name="examples"></a>示例  
  
### <a name="a-inserting-element-nodes-into-the-document"></a>A. 将元素节点插入文档中  
 以下示例说明了如何将元素插入文档中。 首先，将 XML 文档分配给变量的**xml**类型。 然后，通过几个**插入**XML DML 语句，该示例演示了如何在文档中插入元素节点。 每次插入后，SELECT 语句都会显示结果。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;         
SET @myDoc = '<Root>         
    <ProductDescription ProductID="1" ProductName="Road Bike">         
        <Features>         
        </Features>         
    </ProductDescription>         
</Root>'  ;       
SELECT @myDoc;     
-- insert first feature child (no need to specify as first or as last)         
SET @myDoc.modify('         
insert <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>   
into (/Root/ProductDescription/Features)[1]') ;  
SELECT @myDoc ;        
-- insert second feature. We want this to be the first in sequence so use 'as first'         
set @myDoc.modify('         
insert <Warranty>1 year parts and labor</Warranty>          
as first         
into (/Root/ProductDescription/Features)[1]         
')  ;       
SELECT @myDoc  ;       
-- insert third feature child. This one is the last child of <Features> so use 'as last'         
SELECT @myDoc         
SET @myDoc.modify('         
insert <Material>Aluminium</Material>          
as last         
into (/Root/ProductDescription/Features)[1]         
')         
SELECT @myDoc ;        
-- Add fourth feature - this time as a sibling (and not a child)         
-- 'after' keyword is used (instead of as first or as last child)         
SELECT @myDoc  ;       
set @myDoc.modify('         
insert <BikeFrame>Strong long lasting</BikeFrame>   
after (/Root/ProductDescription/Features/Material)[1]         
')  ;       
SELECT @myDoc;  
GO  
```  
  
 请注意，此示例中的各种路径表达式都指定“[1]”以要求每次只返回单个目标。 这样就确保了只有单个目标节点。  
  
### <a name="b-inserting-multiple-elements-into-the-document"></a>B. 将多个元素插入文档中  
 在下面的示例中，文档首先分配给变量的**xml**类型。 然后，将的两个元素，表示产品功能有关，序列分配给第二个变量的**xml**类型。 再将此序列插入第一个变量。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc = N'<Root>             
<ProductDescription ProductID="1" ProductName="Road Bike">             
    <Features> </Features>             
</ProductDescription>             
</Root>';  
DECLARE @newFeatures xml;  
SET @newFeatures = N'<Warranty>1 year parts and labor</Warranty>            
<Maintenance>3 year parts and labor extended maintenance is available</Maintenance>';           
-- insert new features from specified variable            
SET @myDoc.modify('             
insert sql:variable("@newFeatures")             
into (/Root/ProductDescription/Features)[1] ')             
SELECT @myDoc;  
GO  
```  
  
### <a name="c-inserting-attributes-into-a-document"></a>C. 将属性插入文档中  
 下面的示例演示如何在文档中插入属性。首先，文档分配给**xml**类型变量。 然后，一系列**插入**XML DML 语句用于插入到文档中的属性。 每次插入属性后，SELECT 语句都会显示结果。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml ;            
SET @myDoc =   
'<Root>             
    <Location LocationID="10" >             
        <step>Manufacturing step 1 at this work center</step>             
        <step>Manufacturing step 2 at this work center</step>             
    </Location>             
</Root>' ;  
SELECT @myDoc  ;          
-- insert LaborHours attribute             
SET @myDoc.modify('             
insert attribute LaborHours {".5" }             
into (/Root/Location[@LocationID=10])[1] ') ;           
SELECT @myDoc  ;          
-- insert MachineHours attribute but its value is retrived from a sql variable @Hrs             
DECLARE @Hrs float ;            
SET @Hrs =.2   ;          
SET @myDoc.modify('             
insert attribute MachineHours {sql:variable("@Hrs") }             
into   (/Root/Location[@LocationID=10])[1] ');            
SELECT @myDoc;             
-- insert sequence of attribute nodes (note the use of ',' and ()              
-- around the attributes.             
SET @myDoc.modify('             
insert (              
           attribute SetupHours {".5" },             
           attribute SomeOtherAtt {".2"}             
        )             
into (/Root/Location[@LocationID=10])[1] ');             
SELECT @myDoc;  
GO  
```  
  
### <a name="d-inserting-a-comment-node"></a>D. 插入注释节点  
 在此查询中，XML 文档首先分配给变量的**xml**类型。 然后，使用 XML DML 将注释节点插入到第一个 <`step`> 元素后。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;             
SET @myDoc =   
'<Root>             
    <Location LocationID="10" >             
        <step>Manufacturing step 1 at this work center</step>             
        <step>Manufacturing step 2 at this work center</step>             
    </Location>             
</Root>' ;           
SELECT @myDoc;             
SET @myDoc.modify('             
insert <!-- some comment -->             
after (/Root/Location[@LocationID=10]/step[1])[1] ');            
SELECT @myDoc;  
GO  
```  
  
### <a name="e-inserting-a-processing-instruction"></a>E. 插入处理指令  
 在下面的查询中，XML 文档首先分配给变量的**xml**类型。 然后，使用 XML DML 关键字将处理指令插入文档的开头。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc =   
'<Root>   
    <Location LocationID="10" >   
        <step>Manufacturing step 1 at this work center</step>   
        <step>Manufacturing step 2 at this work center</step>   
    </Location>   
</Root>' ;  
SELECT @myDoc ;  
SET @myDoc.modify('   
insert <?Program = "Instructions.exe" ?>   
before (/Root)[1] ') ;  
SELECT @myDoc ;  
GO  
```  
  
### <a name="f-inserting-data-using-a-cdata-section"></a>F. 使用 CDATA 部分插入数据  
 当插入的文本包含在 XML 中无效的字符（如 < 或 >）时，可以使用 CDATA 部分插入数据，如以下查询中所示。 该查询指定一个 CDATA 部分，但该部分作为文本节点添加进来，其中的无效字符转换成实体。 例如，< 另存为&lt;。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;             
SET @myDoc =   
'<Root>             
    <ProductDescription ProductID="1" ProductName="Road Bike">             
        <Features> </Features>             
    </ProductDescription>             
</Root>' ;            
SELECT @myDoc ;            
SET @myDoc.modify('             
insert <![CDATA[ <notxml> as text </notxml> or cdata ]]>   
into  (/Root/ProductDescription/Features)[1] ') ;   
SELECT @myDoc ;  
GO  
```  
  
 查询将文本节点插入 <`Features`> 元素中：  
  
```  
<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features> <notxml> as text </notxml> or cdata </Features>  
</ProductDescription>  
</Root>       
```  
  
### <a name="g-inserting-text-node"></a>G. 插入文本节点  
 在此查询中，XML 文档首先分配给变量的**xml**类型。 然后，使用 XML DML 将文本节点插入为 <`Root`> 元素的第一个子元素。 并使用文本构造函数指定文本。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  
</Features>  
</ProductDescription>  
</Root>'  
SELECT @myDoc;  
set @myDoc.modify('  
 insert text{"Product Catalog Description"}   
 as first into (/Root)[1]  
');  
SELECT @myDoc;  
```  
  
### <a name="h-inserting-a-new-element-into-an-untyped-xml-column"></a>H. 将新元素插入非类型化的 xml 列  
 下面的示例应用来更新存储在 XML 实例的 XML DML **xml**类型列：  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE T (i int, x xml);  
go  
INSERT INTO T VALUES(1,'<Root>  
    <ProductDescription ProductID="1" ProductName="Road Bike">  
        <Features>  
            <Warranty>1 year parts and labor</Warranty>  
            <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
        </Features>  
    </ProductDescription>  
</Root>');  
go  
-- insert a new element  
UPDATE T  
SET x.modify('insert <Material>Aluminium</Material> as first  
  into   (/Root/ProductDescription/Features)[1]  
');  
GO  
```  
  
 此外，当插入 <`Material`> 元素节点时，路径表达式必须返回单个目标。 这通过在表达式结尾处添加 [1] 来显式指定。  
  
```  
-- check the update  
SELECT x.query(' //ProductDescription/Features')  
FROM T;  
GO  
```  
  
### <a name="i-inserting-based-on-an-if-condition-statement"></a>I. 根据 if 条件语句进行插入  
 在下面的示例中，如果条件指定为属于中 Expression1**插入**XML DML 语句。 如果条件为 True，则将属性添加到 <`WorkCenter`> 元素中。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc =   
'<Root>  
    <Location LocationID="10" LaborHours="1.2" >  
        <step>Manufacturing step 1 at this work center</step>  
    <step>Manufacturing step 2 at this work center</step>  
    </Location>  
</Root>';  
SELECT @myDoc  
SET @myDoc.modify('  
insert  
if (/Root/Location[@LocationID=10])  
then attribute MachineHours {".5"}  
else ()  
    as first into   (/Root/Location[@LocationID=10])[1] ');  
SELECT @myDoc;  
GO  
```  
  
 下面的示例非常相似，只不过**插入**XML DML 语句在文档中插入一个元素，如果该条件为 True。 也就是说，如果 <`WorkCenter`> 元素的 <`step`> 子元素少于或等于两个，则在文档中插入元素。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @myDoc xml;  
SET @myDoc =   
'<Root>  
    <Location LocationID="10" LaborHours="1.2" >  
        <step>Manufacturing step 1 at this work center</step>  
        <step>Manufacturing step 2 at this work center</step>  
    </Location>  
</Root>';  
SELECT @myDoc;  
SET @myDoc.modify('  
insert  
if (count(/Root/Location/step) <= 2)  
then element step { "This is a new step" }  
else ()  
    as last into   (/Root/Location[@LocationID=10])[1] ');  
SELECT @myDoc;  
GO  
```  
  
 结果如下：  
  
```  
<Root>  
 <WorkCenter WorkCenterID="10" LaborHours="1.2">  
  <step>Manufacturing step 1 at this work center</step>  
  <step>Manufacturing step 2 at this work center</step>  
  <step>This is a new step</step>  
 </WorkCenter>  
```  
  
### <a name="j-inserting-nodes-in-a-typed-xml-column"></a>J. 将节点插入类型化的 xml 列中  
 此示例将元素和属性插入到 XML 存储在类型化生产说明**xml**列。  
  
 在示例中，你先创建一个表 (T，) 对于类型化**xml** AdventureWorks 数据库中的列。 然后将一个生产说明 XML 实例从 ProductModel 表的 Instructions 列复制到表 T 中。随后再对表 T 中的 XML 内容应用插入操作。  
  
```  
USE AdventureWorks;  
GO            
DROP TABLE T;  
GO             
CREATE TABLE T(ProductModelID int primary key,    
Instructions xml (Production.ManuInstructionsSchemaCollection));  
GO  
INSERT T              
    SELECT ProductModelID, Instructions             
    FROM Production.ProductModel             
    WHERE ProductModelID=7;  
GO             
SELECT Instructions             
FROM T;  
-- now insertion begins             
--1) insert a new manu. Location. The <Root> specified as              
-- expression 2 in the insert() must be singleton.      
UPDATE T   
set Instructions.modify('   
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
insert <MI:Location LocationID="1000" >   
           <MI:step>New instructions go here</MI:step>   
         </MI:Location>   
as first   
into   (/MI:root)[1]   
') ;  
  
SELECT Instructions             
FROM T ;  
-- 2) insert attributes in the new <Location>             
UPDATE T             
SET Instructions.modify('             
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";             
insert attribute LaborHours { "1000" }             
into (/MI:root/MI:Location[@LocationID=1000])[1] ');   
GO             
SELECT Instructions             
FROM T ;  
GO             
--cleanup             
DROP TABLE T ;  
GO             
```  
  
## <a name="see-also"></a>另请参阅  
 [类型化的 XML 与非类型化的 XML 的比较](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [创建 XML 数据的实例](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 数据类型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 数据修改语言 &#40;XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  

