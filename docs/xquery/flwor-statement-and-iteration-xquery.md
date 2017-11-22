---
title: "FLWOR 语句和迭代 (XQuery) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- return clause
- FLWOR statement
- effective Boolean value [XQuery]
- multiple variable binding
- order by clause [XQuery]
- for clause [XQuery]
- where clause [XQuery]
- iterations [XQuery]
- XQuery, FLWOR statement
- EBV
ms.assetid: d7cd0ec9-334a-4564-bda9-83487b6865cb
caps.latest.revision: "44"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a329436ac7ded9f64f0ad0ad4683569ec6f71c9a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="flwor-statement-and-iteration-xquery"></a>FLWOR 语句和迭代 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery 定义了 FLWOR 迭代语法。 FLWOR 是 `for`、`let`、`where`、`order by` 和 `return` 的缩写词。  
  
 FLWOR 语句由以下几个部分组成：  
  
-   用于将一个或多个迭代器变量绑定到输入序列的一个或多个 FOR 子句。  
  
     输入序列可以是其他 XQuery 表达式，例如 XPath 表达式。 它们既可以是节点序列也可以是原子值序列。 原子值序列可以使用文字或构造函数来构造。 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，不允许使用 XML 构造节点作为输入序列。  
  
-   可选的 `let` 子句。 该子句将一个值分配给用于特定迭代的给定变量。 分配的表达式可以为 XQuery 表达式（如 XPath 表达式），并可返回一个节点序列或一个原子值序列。 原子值序列可以通过使用文字或构造函数来构造。 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，不允许使用 XML 构造节点作为输入序列。  
  
-   迭代器变量。 通过使用 `as` 关键字，此变量可包含一个可选的类型判断。  
  
-   可选的 `where` 子句。 此子句将对迭代应用筛选谓词。  
  
-   可选的 `order by` 子句。  
  
-   `return` 表达式。 `return` 子句中的表达式用于构造 FLWOR 语句的结果。  
  
 例如，以下查询将在第一个生产位置对 <`Step`> 元素进行迭代，并返回 <`Step`> 节点的字符串值：  
  
```  
declare @x xml  
set @x='<ManuInstructions ProductModelID="1" ProductModelName="SomeBike" >  
<Location LocationID="L1" >  
  <Step>Manu step 1 at Loc 1</Step>  
  <Step>Manu step 2 at Loc 1</Step>  
  <Step>Manu step 3 at Loc 1</Step>  
</Location>  
<Location LocationID="L2" >  
  <Step>Manu step 1 at Loc 2</Step>  
  <Step>Manu step 2 at Loc 2</Step>  
  <Step>Manu step 3 at Loc 2</Step>  
</Location>  
</ManuInstructions>'  
SELECT @x.query('  
   for $step in /ManuInstructions/Location[1]/Step  
   return string($step)  
')  
```  
  
 结果如下：  
  
```  
Manu step 1 at Loc 1 Manu step 2 at Loc 1 Manu step 3 at Loc 1  
```  
  
 以下查询与上一个查询相似，只不过它是针对 ProductModel 表中的 Instructions 列（类型化的 xml 列）指定的。 此查询将在指定产品的第一个生产车间对所有生产步骤（<`step`> 元素）进行迭代。  
  
```  
SELECT Instructions.query('  
   declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $Step in //AWMI:root/AWMI:Location[1]/AWMI:step  
      return  
           string($Step)   
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 请注意上述查询的以下方面：  
  
-   `$Step` 是迭代器变量。  
  
-   [路径表达式](../xquery/path-expressions-xquery.md)， `//AWMI:root/AWMI:Location[1]/AWMI:step`，生成输入的序列。 此序列是第一个 <`Location`> 元素节点的 <`step`> 子元素节点序列。  
  
-   不使用可选的谓词子句 `where`。  
  
-   `return` 表达式将从 <`step`> 元素返回字符串值。  
  
 [字符串函数 (XQuery)](../xquery/data-accessor-functions-string-xquery.md)用于检索的字符串值 <`step`> 节点。  
  
 下面是部分结果：  
  
```  
Insert aluminum sheet MS-2341 into the T-85A framing tool.   
Attach Trim Jig TJ-26 to the upper and lower right corners of   
the aluminum sheet. ....         
```  
  
 以下是其他允许使用的输入序列的示例：  
  
```  
declare @x xml  
set @x=''  
SELECT @x.query('  
for $a in (1, 2, 3)  
  return $a')  
-- result = 1 2 3   
  
declare @x xml  
set @x=''  
SELECT @x.query('  
for $a in   
   for $b in (1, 2, 3)  
      return $b  
return $a')  
-- result = 1 2 3  
  
declare @x xml  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('  
  for $a in (xs:string( "test"), xs:double( "12" ), data(/ROOT/a ))  
  return $a')  
-- result test 12 111  
```  
  
 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，不允许使用异类序列。 尤其不允许使用由原子值和节点混合组成的序列。  
  
 迭代经常使用连同[XML 构造](../xquery/xml-construction-xquery.md)中将 XML 转换的语法格式，如第二个查询中所示。  
  
 在 AdventureWorks 示例数据库中，生产说明存储在**说明**列**Production.ProductModel**表具有以下形式：  
  
```  
<Location LocationID="10" LaborHours="1.2"   
            SetupHours=".2" MachineHours=".1">  
  <step>describes 1st manu step</step>  
   <step>describes 2nd manu step</step>  
   ...  
</Location>  
...  
```  
  
 以下查询将构造新的 XML，其中将 <`Location`> 元素与生产车间属性一起作为子元素返回。  
  
```  
<Location>  
   <LocationID>10</LocationID>  
   <LaborHours>1.2</LaborHours>  
   <SetupHours>.2</SteupHours>  
   <MachineHours>.1</MachineHours>  
</Location>  
...  
```  
  
 以下是查询语句：  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $WC in /AWMI:root/AWMI:Location  
        return  
          <Location>  
            <LocationID> { data($WC/@LocationID) } </LocationID>  
            <LaborHours>   { data($WC/@LaborHours) }   </LaborHours>  
            <SetupHours>   { data($WC/@SetupHours) }   </SetupHours>  
            <MachineHours> { data($WC/@MachineHours) } </MachineHours>  
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 请注意上述查询的以下方面：  
  
-   FLWOR 语句将为特定产品检索 <`Location`> 元素序列。  
  
-   [数据函数 (XQuery)](../xquery/data-accessor-functions-data-xquery.md)用于提取每个属性的值，因此它们将将添加到生成的 XML 作为而不是作为属性的文本节点。  
  
-   RETURN 子句中的表达式将构造所需的 XML。  
  
 下面是部分结果：  
  
```  
<Location>  
  <LocationID>10</LocationID>  
  <LaborHours>2.5</LaborHours>  
  <SetupHours>0.5</SetupHours>  
  <MachineHours>3</MachineHours>  
</Location>  
<Location>  
   ...  
<Location>  
...  
```  
  
## <a name="using-the-let-clause"></a>使用 let 子句  
 可以使用 `let` 子句来命名可通过引用变量来引用的重复表达式。 每次在查询中引用 `let` 变量时，都会将分配给该变量的表达式插入到查询中。 也就是说，引用该表达式多少次，就执行多少次此语句。  
  
 在 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 数据库中，生产说明包含有关所需的工具以及在何处使用这些工具的信息。 以下查询使用 `let` 子句列出构建生产模型所需的工具以及各工具的使用位置。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $T in //AWMI:tool  
            let $L := //AWMI:Location[.//AWMI:tool[.=data($T)]]  
        return  
          <tool desc="{data($T)}" Locations="{data($L/@LocationID)}"/>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
## <a name="using-the-where-clause"></a>使用 where 子句  
 可以使用 `where` 子句来筛选迭代结果。 下面的示例说明了这一点。  
  
 在生产自行车时，生产过程经过了一系列生产车间。 每个生产车间定义一个生产步骤序列。 以下查询仅检索那些生产某个自行车型号并且生产步骤少于三步的生产车间。 即，它们包含的 <`step`> 元素少于三个。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location  
      where count($WC/AWMI:step) < 3  
      return  
          <Location >  
           { $WC/@LocationID }   
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 请注意上述查询的以下方面：  
  
-   `where`关键字使用**count （)**函数来计算的数量 <`step`> 子元素中每个工作中心位置。  
  
-   `return` 表达式将构造您希望从迭代结果生成的 XML。  
  
 结果如下：  
  
```  
<Location LocationID="30"/>   
```  
  
 `where` 子句中的表达式的结果使用下列规则按指定的顺序转换为布尔值。 这些规则与路径表达式中的谓词规则相同，只不过不允许使用整数：  
  
1.  如果 `where` 表达式返回一个空序列，则其有效的布尔值为 False。  
  
2.  如果 `where` 表达式返回一个简单的布尔类型值，则该值为有效的布尔值。  
  
3.  如果 `where` 表达式返回至少包含一个节点的序列，则有效的布尔值为 True。  
  
4.  否则，它将出现静态错误。  
  
## <a name="multiple-variable-binding-in-flwor"></a>FLWOR 中的多个变量绑定  
 可以用单个 FLWOR 表达式将多个变量绑定到输入序列。 在下面的示例中，查询针对非类型化的 xml 变量指定。 FLOWR 表达式将返回每个 <`Location`> 元素中的第一个 <`Step`> 子元素。  
  
```  
declare @x xml  
set @x='<ManuInstructions ProductModelID="1" ProductModelName="SomeBike" >  
<Location LocationID="L1" >  
  <Step>Manu step 1 at Loc 1</Step>  
  <Step>Manu step 2 at Loc 1</Step>  
  <Step>Manu step 3 at Loc 1</Step>  
</Location>  
<Location LocationID="L2" >  
  <Step>Manu step 1 at Loc 2</Step>  
  <Step>Manu step 2 at Loc 2</Step>  
  <Step>Manu step 3 at Loc 2</Step>  
</Location>  
</ManuInstructions>'  
SELECT @x.query('  
   for $Loc in /ManuInstructions/Location,  
       $FirstStep in $Loc/Step[1]  
   return   
       string($FirstStep)  
')  
```  
  
 请注意上述查询的以下方面：  
  
-   `for`表达式定义`$Loc`和 $`FirstStep`变量。  
  
-   `two` 和 `/ManuInstructions/Location` `$FirstStep in $Loc/Step[1]` 表达式相互关联，`$FirstStep` 的值取决于 `$Loc` 的值。  
  
-   与 `$Loc` 相关联的表达式将生成一个 <`Location`> 元素序列。 针对每个 <`Location`> 元素，`$FirstStep` 将生成包含一个 <`Step`> 元素（单一实例）的序列。  
  
-   `$Loc` 在与 `$FirstStep` 变量相关联的表达式中指定。  
  
 结果如下：  
  
```  
Manu step 1 at Loc 1   
Manu step 1 at Loc 2  
```  
  
 下面的查询是类似，只不过它针对 Instructions 列中，键入指定**xml**列中的**ProductModel**表。 [XML 构造 (XQuery)](../xquery/xml-construction-xquery.md)用于生成所需的 XML。  
  
```  
SELECT Instructions.query('  
     declare default element namespace "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /root/Location,  
            $S  in $WC/step  
      return  
          <Step LocationID= "{$WC/@LocationID }" >  
            { $S/node() }  
          </Step>  
') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 请注意上述查询的以下方面：  
  
-   `for` 子句定义了两个变量：`$WC` 和 `$S`。 在生产某个自行车产品型号时，与 `$WC` 相关联的表达式将生成一系列生产车间。 分配给 `$S` 变量的路径表达式将为 `$WC` 中的每个生产车间序列生成一个相应的步骤序列。  
  
-   Return 语句构造具有的 XML <`Step`> 元素包含生产步骤和**LocationID**作为其属性。  
  
-   **声明默认元素命名空间**以便得到的 XML 中的所有命名空间声明显示在顶级元素，XQuery prolog 中使用。 这使结果的可读性更强。 有关默认命名空间的详细信息，请参阅[处理在 XQuery 中的命名空间](../xquery/handling-namespaces-in-xquery.md)。  
  
 下面是部分结果：  
  
```  
<Step xmlns=  
    "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"     
  LocationID="10">  
     Insert <material>aluminum sheet MS-2341</material> into the <tool>T-   
     85A framing tool</tool>.   
</Step>  
...  
<Step xmlns=  
      "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"     
    LocationID="20">  
        Assemble all frame components following blueprint   
        <blueprint>1299</blueprint>.  
</Step>  
...  
```  
  
## <a name="using-the-order-by-clause"></a>使用 order by 子句  
 通过使用 FLWOR 表达式中的 `order by` 子句可在 XQuery 中进行排序。 排序表达式传递给`order by`子句必须返回其类型对有效值**gt**运算符。 每个排序表达式必须针对每一项生成一个单独的序列。 默认情况下，按升序进行排序。 您也可以选择为每个排序表达式指定升序或降序顺序。  
  
> [!NOTE]  
>  通过在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中实现 XQuery 进行的字符串值的排序比较始终是使用二进制 Unicode 码位排序规则来执行的。  
  
 以下查询将从 AdditionalContactInfo 列检索有关特定客户的所有电话号码。 结果按电话号码进行排序。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT AdditionalContactInfo.query('  
   declare namespace act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
   declare namespace aci="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
   for $a in /aci:AdditionalContactInfo//act:telephoneNumber   
   order by $a/act:number[1] descending  
   return $a  
') As Result  
FROM Person.Person  
WHERE BusinessEntityID=291;  
```  
  
 请注意，[原子化 (XQuery)](../xquery/atomization-xquery.md)过程中检索的原子值 <`number`> 元素之前将其传递给`order by`。 你可以通过使用编写表达式**data （)**函数，但不需要。  
  
```  
order by data($a/act:number[1]) descending  
```  
  
 结果如下：  
  
```  
<act:telephoneNumber xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3334</act:number>  
</act:telephoneNumber>  
<act:telephoneNumber xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3333</act:number>  
</act:telephoneNumber>  
```  
  
 可以使用 WITH XMLNAMESPACES 声明命名空间，而不是在查询 prolog 中声明。  
  
```  
WITH XMLNAMESPACES (  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo'  AS aci)  
  
SELECT AdditionalContactInfo.query('  
   for $a in /aci:AdditionalContactInfo//act:telephoneNumber   
   order by $a/act:number[1] descending  
   return $a  
') As Result  
FROM Person.Person  
WHERE BusinessEntityID=291;  
```  
  
 还可以按属性值进行排序。 例如，以下查询将检索新创建的 <`Location`> 元素，其中包含按 LaborHours 属性以降序顺序排序的 LocationID 和 LaborHours 属性。 结果，将首先返回工时最长的生产车间。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location   
order by $WC/@LaborHours descending  
        return  
          <Location>  
             { $WC/@LocationID }   
             { $WC/@LaborHours }   
          </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 结果如下：  
  
```  
<Location LocationID="60" LaborHours="4"/>  
<Location LocationID="50" LaborHours="3"/>  
<Location LocationID="10" LaborHours="2.5"/>  
<Location LocationID="20" LaborHours="1.75"/>  
<Location LocationID="30" LaborHours="1"/>  
<Location LocationID="45" LaborHours=".5"/>  
```  
  
 在以下查询中，将按元素名称对结果进行排序。 此查询将从产品目录中检索特定产品的规范。 这些规范是 <`Specifications`> 元素的子元素。  
  
```  
SELECT CatalogDescription.query('  
     declare namespace  
 pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $a in /pd:ProductDescription/pd:Specifications/*   
     order by local-name($a)  
      return $a  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19;  
```  
  
 请注意上述查询的以下方面：  
  
-   `/p1:ProductDescription/p1:Specifications/*` 表达式将返回 <`Specifications`> 元素的子元素。  
  
-   `order by (local-name($a))` 表达式将按元素名称的本地部分对序列进行排序。  
  
 结果如下：  
  
```  
<Color>Available in most colors</Color>  
<Material>Almuminum Alloy</Material>  
<ProductLine>Mountain bike</ProductLine>  
<RiderExperience>Advanced to Professional riders</RiderExperience>  
<Style>Unisex</Style>    
```  
  
 其排序表达式返回空值的节点将被列在序列的开头，如以下示例中所示：  
  
```  
declare @x xml  
set @x='<root>  
  <Person Name="A" />  
  <Person />  
  <Person Name="B" />  
</root>  
'  
select @x.query('  
  for $person in //Person  
  order by $person/@Name  
  return   $person  
')  
```  
  
 结果如下：  
  
```  
<Person />  
<Person Name="A" />  
<Person Name="B" />  
```  
  
 您可以指定多个排序条件，如以下示例中所示。 此示例中的查询将先按 Title 属性值再按 Administrator 属性值对 <`Employee`> 元素进行排序。  
  
```  
declare @x xml  
set @x='<root>  
  <Employee ID="10" Title="Teacher"        Gender="M" />  
  <Employee ID="15" Title="Teacher"  Gender="F" />  
  <Employee ID="5" Title="Teacher"         Gender="M" />  
  <Employee ID="11" Title="Teacher"        Gender="F" />  
  <Employee ID="8" Title="Administrator"   Gender="M" />  
  <Employee ID="4" Title="Administrator"   Gender="F" />  
  <Employee ID="3" Title="Teacher"         Gender="F" />  
  <Employee ID="125" Title="Administrator" Gender="F" /></root>'  
SELECT @x.query('for $e in /root/Employee  
order by $e/@Title ascending, $e/@Gender descending  
  
  return  
     $e  
')  
```  
  
 结果如下：  
  
```  
<Employee ID="8" Title="Administrator" Gender="M" />  
<Employee ID="4" Title="Administrator" Gender="F" />  
<Employee ID="125" Title="Administrator" Gender="F" />  
<Employee ID="10" Title="Teacher" Gender="M" />  
<Employee ID="5" Title="Teacher" Gender="M" />  
<Employee ID="11" Title="Teacher" Gender="F" />  
<Employee ID="15" Title="Teacher" Gender="F" />  
<Employee ID="3" Title="Teacher" Gender="F" />  
```  
  
### <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   排序表达式必须经过同类类型化。 这是通过静态检查来确定的。  
  
-   无法控制对空序列的排序。  
  
-   不支持对 `order by` 使用 empty least、empty greatest 和 collation 关键字  
  
## <a name="see-also"></a>另请参阅  
 [XQuery 表达式](../xquery/xquery-expressions.md)  
  
  
