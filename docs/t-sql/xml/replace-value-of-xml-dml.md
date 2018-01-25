---
title: "替换值 (XML DML) |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- XML DML [SQL Server]
- update keyword
- replacement values [XML DML]
- updating node values
- replace value of XML DML statement
ms.assetid: c310f6df-7adf-493b-b56b-8e3143b13ae7
caps.latest.revision: "28"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 236e919d1817e100c043e29de94c25442aac776f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="replace-value-of-xml-dml"></a>替换 (XML DML) 的值
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在文档中更新节点的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
replace value of Expression1   
with Expression2  
```  
  
## <a name="arguments"></a>参数  
 *Expression1*  
 标识其值要更新的节点。 它必须仅标识一个单个节点。 也就是说， *Expression1*必须 statical 单一实例。 如果 XML 已类型化，则节点的类型必须是简单类型。 如果选择了多个节点，则会出现错误。 如果*Expression1*返回的返回空序列，没有值替换发生，并且没有错误。 *Expression1*必须返回一个元素，只需键入的内容 （列表或原子类型）、 一个文本节点或属性节点。 *Expression1*不能是联合类型、 复杂类型、 处理指令、 文档节点中或注释节点。 如果它是，则会返回错误。  
  
 *Expression2*  
 标识节点的新值。 这可以是一个表达式，返回一个只需类型化的节点，因为**data （)**将隐式使用。 如果值为的值，列表**更新**语句会替换旧值列表。 在对类型化的 XML 实例中，修改*Expression2*必须是相同类型或子类型的*表达式*1。 否则，将返回错误。 修改非类型化的 XML 实例， *Expression2*必须可以原子化的表达式。 否则，将返回错误。  
  
## <a name="examples"></a>示例  
 下面的示例**替换值**XML DML 语句演示了如何更新 XML 文档中的节点。  
  
### <a name="a-replacing-values-in-an-xml-instance"></a>A. 在 XML 实例中替换值  
 在下面的示例中，文档实例第一次分配给变量的**xml**类型。 然后，**替换值**XML DML 语句更新文档中的值。  
  
```  
DECLARE @myDoc xml;  
SET @myDoc = '<Root>  
<Location LocationID="10"   
            LaborHours="1.1"  
            MachineHours=".2" >Manufacturing steps are described here.  
<step>Manufacturing step 1 at this work center</step>  
<step>Manufacturing step 2 at this work center</step>  
</Location>  
</Root>';  
SELECT @myDoc;  
  
-- update text in the first manufacturing step  
SET @myDoc.modify('  
  replace value of (/Root/Location/step[1]/text())[1]  
  with     "new text describing the manu step"  
');  
SELECT @myDoc;  
-- update attribute value  
SET @myDoc.modify('  
  replace value of (/Root/Location/@LaborHours)[1]  
  with     "100.0"  
');  
SELECT @myDoc;  
```  
  
 请注意，更新的目标必须最多是一个通过在表达式的结尾添加“[1]”在路径表达式中显式指定的节点。  
  
### <a name="b-using-the-if-expression-to-determine-replacement-value"></a>B. 使用 if 表达式以确定替换值  
 你可以指定**如果**表达式中的 Expression2**替换值的 XML DML**语句，如下面的示例中所示。 Expression1 标识第一个生产车间的 LaborHours 属性将要更新。 Expression2 使用**如果**表达式以确定 LaborHours 属性的新值。  
  
```  
DECLARE @myDoc xml  
SET @myDoc = '<Root>  
<Location LocationID="10"   
            LaborHours=".1"  
            MachineHours=".2" >Manu steps are described here.  
<step>Manufacturing step 1 at this work center</step>  
<step>Manufacturing step 2 at this work center</step>  
</Location>  
</Root>'  
--SELECT @myDoc  
  
SET @myDoc.modify('  
  replace value of (/Root/Location[1]/@LaborHours)[1]  
  with (  
       if (count(/Root/Location[1]/step) > 3) then  
         "3.0"  
       else  
          "1.0"  
      )  
')  
SELECT @myDoc  
```  
  
### <a name="c-updating-xml-stored-in-an-untyped-xml-column"></a>C. 更新存储在非类型化的 XML 列中的 XML  
 以下示例更新存储在列中的 XML：  
  
```  
drop table T  
go  
CREATE TABLE T (i int, x xml)  
go  
INSERT INTO T VALUES(1,'<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>')  
go  
-- verify the current <ProductDescription> element  
SELECT x.query(' /Root/ProductDescription')  
FROM T  
-- update the ProductName attribute value  
UPDATE T  
SET x.modify('  
  replace value of (/Root/ProductDescription/@ProductName)[1]  
  with "New Road Bike" ')  
-- verify the update  
SELECT x.query(' /Root/ProductDescription')  
FROM T  
```  
  
### <a name="d-updating-xml-stored-in-a-typed-xml-column"></a>D. 更新存储在类型化的 XML 列中的 XML  
 此示例替换存储在类型化的 XML 列中的生产说明文档中的值。  
  
 在该示例中，首先在 AdventureWorks 数据库中创建带有类型化的 XML 列的表 (T)。 然后将一个生产说明 XML 实例从 ProductModel 表的 Instructions 列复制到表 T 中。随后再对表 T 中的 XML 内容应用插入操作。  
  
```  
use AdventureWorks  
go  
drop table T  
go  
create table T(ProductModelID int primary key,   
Instructions xml (Production.ManuInstructionsSchemaCollection))  
go  
insert  T   
select ProductModelID, Instructions  
from Production.ProductModel  
where ProductModelID=7  
go  
--insert a new location - <Location 1000/>.   
update T  
set Instructions.modify('  
  declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
insert <MI:Location LocationID="1000"  LaborHours="1000"  LotSize="1000" >  
           <MI:step>Do something using <MI:tool>hammer</MI:tool></MI:step>  
         </MI:Location>  
  as first  
  into   (/MI:root)[1]  
')  
go  
select Instructions  
from T  
go  
-- Now replace manu. tool in location 1000  
update T  
set Instructions.modify('  
  declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  replace value of (/MI:root/MI:Location/MI:step/MI:tool)[1]   
  with   "screwdriver"  
')  
go  
select Instructions  
from T  
-- Now replace value of lot size  
update T  
set Instructions.modify('  
  declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  replace value of (/MI:root/MI:Location/@LotSize)[1]   
  with   500 cast as xs:decimal ?  
')  
go  
select Instructions  
from T  
```  
  
 请注意，使用**强制转换**替换 LotSize 值时。 当该值必须为特定类型时这是必需。 在此示例中，如果值为 500，则显式转换是不必要的。  
  
## <a name="see-also"></a>另请参阅  
 [类型化的 XML 与非类型化的 XML 的比较](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [创建 XML 数据的实例](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [XML 数据类型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 数据修改语言 &#40;XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
