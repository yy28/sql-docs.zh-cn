---
title: "SequenceType 表达式 (XQuery) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- SequenceType expressions
- instance of operator [XQuery]
- expressions [XQuery], SequenceType
- cast as operator
ms.assetid: ad3573da-d820-4d1c-81c4-a83c4640ce22
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ac481d608106e5ce787ffe737d8d11fda67af3fb
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="sequencetype-expressions-xquery"></a>SequenceType 表达式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 XQuery 中，值始终是序列。 值类型称为序列类型。 序列类型可用在**实例**XQuery 表达式。 当需要引用 XQuery 表达式中的类型时，将使用 XQuery 规范中说明的 SequenceType 语法。  
  
 原子类型名称还可在**强制转换为**XQuery 表达式。 在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、**实例**和**强制转换为**部分支持 SequenceTypes XQuery 表达式。  
  
## <a name="instance-of-operator"></a>instance of 运算符  
 **实例**运算符可以用于确定指定的表达式的值的动态的或运行时类型。 例如：  
  
```  
  
Expression instance of SequenceType[Occurrence indicator]  
```  
  
 请注意，`instance of`运算符， `Occurrence indicator`，指定的基数，所产生的序列中的项数。 如果未指定，则假定基数为 1。 在[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，仅问号 (**？)**支持发生指示符。 **？** 发生指示符指示`Expression`可以返回零个或一个项。 如果**？** 指定发生指示符，则`instance of`时才返回 True`Expression`类型匹配所指定`SequenceType`，无论`Expression`返回单一实例或空序列。  
  
 如果**？** 未指定发生指示符，`sequence of`返回 True，仅当`Expression`键入匹配`Type`指定和`Expression`返回单一实例。  
  
 **请注意**的加号 (**+**) 和星号 (**\***) 中不支持发生指示符[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
 下面的示例演示如何使用**实例**XQuery 运算符。  
  
### <a name="example-a"></a>示例 A  
 下面的示例创建**xml**类型变量，并指定对它的查询。 查询表达式将指定 `instance of` 运算符以确定第一个操作数返回的值的动态类型是否与第二个操作数中指定的类型相匹配。  
  
 以下查询将返回 True，因为 125 值为指定类型的实例**xs:integer**:  
  
```  
declare @x xml  
set @x=''  
select @x.query('125 instance of xs:integer')  
go  
```  
  
 以下查询将返回 True，因为由第一个操作数中的 /a[1] 表达式返回的值是一个元素：  
  
```  
declare @x xml  
set @x='<a>1</a>'  
select @x.query('/a[1] instance of element()')  
go  
```  
  
 同样，在以下查询中，`instance of` 将返回 True，因为在第一个表达式中表达式的值类型是属性：  
  
```  
declare @x xml  
set @x='<a attr1="x">1</a>'  
select @x.query('/a[1]/@attr1 instance of attribute()')  
go  
```  
  
 在下列示例中，表达式 `data(/a[1]` 将返回类型为 xdt:untypedAtomic 的原子值。 因此，`instance of` 返回 True。  
  
```  
declare @x xml  
set @x='<a>1</a>'  
select @x.query('data(/a[1]) instance of xdt:untypedAtomic')  
go  
```  
  
 在以下查询中，表达式 `data(/a[1]/@attrA` 将返回非类型化的原子值。 因此，`instance of` 返回 True。  
  
```  
declare @x xml  
set @x='<a attrA="X">1</a>'  
select @x.query('data(/a[1]/@attrA) instance of xdt:untypedAtomic')  
go  
```  
  
### <a name="example-b"></a>示例 B  
 在此示例中，将查询 AdventureWorks 示例数据库中的类型化的 XML 列。 类型化信息由与被查询的列关联的 XML 架构集合提供。  
  
 在表达式中， **data （)**返回类型为 xs: string 根据与该列关联的架构 ProductModelID 属性的类型化的值。 因此，`instance of` 返回 True。  
  
```  
SELECT CatalogDescription.query('  
   declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   data(/PD:ProductDescription[1]/@ProductModelID) instance of xs:string  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 有关详细信息，请参阅 [类型化的 XML 与非类型化的 XML 的比较](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)。  
  
 以下查询 usetheBoolean`instance of`表达式以确定 LocationID 属性是否为 xs:integer 类型：  
  
```  
SELECT Instructions.query('  
   declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   /AWMI:root[1]/AWMI:Location[1]/@LocationID instance of attribute(LocationID,xs:integer)  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 对 CatalogDescription 非类型化的 XML 列指定以下查询。 类型化信息由与此列关联的 XML 架构集合提供。  
  
 查询使用 `element(ElementName, ElementType?)` 表达式中的 `instance of` 测试来验证 `/PD:ProductDescription[1]` 是否返回特定名称和类型的元素节点。  
  
```  
SELECT CatalogDescription.query('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /PD:ProductDescription[1] instance of element(PD:ProductDescription, PD:ProductDescription?)  
    ') as Result  
FROM  Production.ProductModel  
where ProductModelID=19  
```  
  
 该查询返回 True。  
  
### <a name="example-c"></a>示例 C  
 使用联合类型时，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 `instance of` 表达式有一个限制：具体来说，当某个元素或属性的类型为联合类型时，`instance of` 可能无法确定其准确的类型。 因此，查询将返回 False，除非用于 SequenceType 中的原子类型在简单类型层次结构中是表达式的实际类型的最高父级。 即以 SequenceType 指定的原子类型必须是任意简单类型的直接子级。 有关类型层次结构的信息，请参阅[在 XQuery 中的类型转换规则](../xquery/type-casting-rules-in-xquery.md)。  
  
 下一个查询示例将执行以下操作：  
  
-   使用联合类型创建 XML 架构集合，在其中定义诸如整数或字符串等类型。  
  
-   声明类型化**xml**变量中使用的 XML 架构集合。  
  
-   将示例 XML 实例分配给变量。  
  
-   查询变量以说明 `instance of` 在处理联合类型时的行为。  
  
 以下是查询语句：  
  
```  
CREATE XML SCHEMA COLLECTION MyTestSchema AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns" xmlns:ns="http://ns">  
<simpleType name="MyUnionType">  
<union memberTypes="integer string"/>  
</simpleType>  
<element name="TestElement" type="ns:MyUnionType"/>  
</schema>'  
Go  
```  
  
 以下查询将返回 False，因为在 `instance of` 表达式中指定的 SequenceType 不是指定表达式的实际类型的最高父级。 即 <`TestElement`> 的值是整数类型。 最高父级为 xs:decimal。 但是，未将它指定为 `instance of` 运算符的第二个操作数。  
  
```  
SET QUOTED_IDENTIFIER ON  
DECLARE @var XML(MyTestSchema)  
  
SET @var = '<TestElement xmlns="http://ns">123</TestElement>'  
  
SELECT @var.query('declare namespace ns="http://ns"   
   data(/ns:TestElement[1]) instance of xs:integer')  
go  
```  
  
 因为 xs:integer 的最高父级是 xs:decimal，所以，如果您要修改查询并在查询中将 xs:decimal 指定为 SequenceType，则查询将返回 True。  
  
```  
SET QUOTED_IDENTIFIER ON  
DECLARE @var XML(MyTestSchema)  
SET @var = '<TestElement xmlns="http://ns">123</TestElement>'  
SELECT @var.query('declare namespace ns="http://ns"     
   data(/ns:TestElement[1]) instance of xs:decimal')  
go  
```  
  
### <a name="example-d"></a>示例 D  
 在此示例中，你首先创建 XML 架构集合并使用它来键入**xml**变量。 类型化**xml**变量然后查询来演示`instance of`功能。  
  
 以下 XML 架构集合定义了一个简单类型 myType 和一个属于 myType 类型的元素 <`root`>：  
  
```  
drop xml schema collection SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="myNS" xmlns:ns="myNS"  
xmlns:s="http://schemas.microsoft.com/sqlserver/2004/sqltypes">  
      <import namespace="http://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
      <simpleType name="myType">  
           <restriction base="s:varchar">  
                  <maxLength value="20"/>  
            </restriction>  
      </simpleType>  
      <element name="root" type="ns:myType"/>  
</schema>'  
Go  
```  
  
 现在，创建类型化**xml**变量和对其进行查询：  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "http://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
   data(/ns:root[1]) instance of ns:myType')  
go  
```  
  
 由于 myType 类型仅限于从 varchar 类型（在 sqltypes 架构中定义）派生，因而 `instance of` 也将返回 True。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "http://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
data(/ns:root[1]) instance of sqltypes:varchar?')  
go  
```  
  
### <a name="example-e"></a>示例 E  
 在下列示例中，表达式将检索 IDREFS 属性的值之一，并使用 `instance of` 来确定该值是否是 IDREF 类型。 该示例执行以下操作：  
  
-   在其中创建 XML 架构集合 <`Customer`> 元素具有**OrderList** IDREFS 类型属性，与 <`Order`> 元素具有**OrderID** ID 类型的特性。  
  
-   创建类型化**xml**变量，并将分配到它的示例 XML 实例。  
  
-   对变量指定查询。 查询表达式将从第一个 <`Customer`> 的 OrderList IDRERS 类型属性中检索第一个顺序 ID 值。 检索的值是 IDREF 类型。 因此， `instance of` ，则返回 True。  
  
```  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:Customers="Customers" targetNamespace="Customers">  
            <element name="Customers" type="Customers:CustomersType"/>  
            <complexType name="CustomersType">  
                        <sequence>  
                            <element name="Customer" type="Customers:CustomerType" minOccurs="0" maxOccurs="unbounded" />  
                        </sequence>  
            </complexType>  
             <complexType name="OrderType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="OrderValue" type="integer" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="OrderID" type="ID" />  
            </complexType>  
  
            <complexType name="CustomerType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="spouse" type="string" minOccurs="0" maxOccurs="unbounded"/>  
                                <element name="Order" type="Customers:OrderType" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="CustomerID" type="string" />  
                <attribute name="OrderList" type="IDREFS" />  
            </complexType>  
 </schema>'  
go  
declare @x xml(SC)  
set @x='<CustOrders:Customers xmlns:CustOrders="Customers">  
                <Customer CustomerID="C1" OrderList="OrderA OrderB"  >  
                              <spouse>Jenny</spouse>  
                                <Order OrderID="OrderA"><OrderValue>11</OrderValue></Order>  
                                <Order OrderID="OrderB"><OrderValue>22</OrderValue></Order>  
  
                </Customer>  
                <Customer CustomerID="C2" OrderList="OrderC OrderD" >  
                                <spouse>John</spouse>  
                                <Order OrderID="OrderC"><OrderValue>33</OrderValue></Order>  
                                <Order OrderID="OrderD"><OrderValue>44</OrderValue></Order>  
  
                        </Customer>  
                <Customer CustomerID="C3"  OrderList="OrderE OrderF" >  
                                <spouse>Jane</spouse>  
                                <Order OrderID="OrderE"><OrderValue>55</OrderValue></Order>  
                                <Order OrderID="OrderF"><OrderValue>55</OrderValue></Order>  
                </Customer>  
                <Customer CustomerID="C4"  OrderList="OrderG"  >  
                                <spouse>Tim</spouse>  
                                <Order OrderID="OrderG"><OrderValue>66</OrderValue></Order>  
                        </Customer>  
                <Customer CustomerID="C5"  >  
                </Customer>  
                <Customer CustomerID="C6" >  
                </Customer>  
                <Customer CustomerID="C7"  >  
                </Customer>  
</CustOrders:Customers>'  
  
select @x.query(' declare namespace CustOrders="Customers";   
 data(CustOrders:Customers/Customer[1]/@OrderList)[1] instance of xs:IDREF ? ') as XML_result  
```  
  
### <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   **Schema-element()**和**schema-attribute()**序列类型不支持与比较`instance of`运算符。  
  
-   不支持完整序列（如 `(1,2) instance of xs:integer*`）。  
  
-   如果要使用的一种形式**element()**序列指定一个类型名称，例如类型`element(ElementName, TypeName)`，该类型必须进行限定用问号 （？）。 例如，`element(Title, xs:string?)` 指示元素可能为空。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]不支持的运行时检测**xsi: nil**属性使用`instance of`。  
  
-   如果 `Expression` 中的值来自类型化为联合类型的元素或属性，则 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 只能识别派生了值类型的非派生的 primitive 类型。 例如，如果 <`e1`> 定义为静态类型 (xs:integer | xs:string)，则下面的语句将返回 False。  
  
    ```  
    data(<e1>123</e1>) instance of xs:integer  
    ```  
  
     而 `data(<e1>123</e1>) instance of xs:decimal` 将返回 True。  
  
-   有关**processing-instruction()**和**document-node()**序列类型允许仅不带参数的窗体。 例如，允许 `processing-instruction()`，但不允许 `processing-instruction('abc')`。  
  
## <a name="cast-as-operator"></a>cast as 运算符  
 **强制转换为**表达式可以用于将值转换为特定的数据类型。 例如：  
  
```  
  
Expression cast as  AtomicType?  
```  
  
 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，要求问号 (?) 在 `AtomicType` 之后。 例如，如下面的查询中所示`"2" cast as xs:integer?`将字符串值转换为整数：  
  
```  
declare @x xml  
set @x=''  
select @x.query('"2" cast as xs:integer?')  
```  
  
 在下面的查询， **data （)**返回 ProductModelID 属性，字符串类型的类型化的值。 `cast as`运算符将值转换为 xs:integer。  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD)  
SELECT CatalogDescription.query('  
   data(/PD:ProductDescription[1]/@ProductModelID) cast as xs:integer?  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 显式使用**data （)**中此查询不需要。 `cast as` 表达式在输入表达式中执行隐式原子化。  
  
### <a name="constructor-functions"></a>构造函数  
 您可以使用原子类型来构造函数。 例如，而不是使用`cast as`运算符， `"2" cast as xs:integer?`，你可以使用**xs:integer()**构造函数中的，如以下示例所示：  
  
```  
declare @x xml  
set @x=''  
select @x.query('xs:integer("2")')  
```  
  
 以下示例返回的 xs:date 值等于 2000-01-01Z。  
  
```  
declare @x xml  
set @x=''  
select @x.query('xs:date("2000-01-01Z")')  
```  
  
 您还可以使用用户定义的原子类型的构造函数。 例如，如果与该 XML 架构集合关联的 XML 数据类型将定义一个简单的类型， **myType()**可以使用构造函数以返回该类型的值。  
  
#### <a name="implementation-limitations"></a>实现限制  
  
-   XQuery 表达式**typeswitch**，**强制转换**，和**将**不支持。  
  
-   **强制转换为**需要一个问号 （？）之后的原子类型。  
  
-   **xs: qname**不支持作为强制转换的类型。 使用**展开 QName**相反。  
  
-   **xs: date**， **xs: time**，和**xs: datetime**需要时区，这将由 a Z。  
  
     以下查询失败，因为未指定时区。  
  
    ```  
    DECLARE @var XML  
    SET @var = ''  
    SELECT @var.query(' <a>{xs:date("2002-05-25")}</a>')  
    go  
    ```  
  
     通过向值添加时区指示符 Z，查询便可正常工作。  
  
    ```  
    DECLARE @var XML  
    SET @var = ''  
    SELECT @var.query(' <a>{xs:date("2002-05-25Z")}</a>')  
    go  
    ```  
  
     结果如下：  
  
    ```  
    <a>2002-05-25Z</a>  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [XQuery 表达式](../xquery/xquery-expressions.md)   
 [类型系统 &#40;XQuery &#41;](../xquery/type-system-xquery.md)  
  
  

