---
title: "类型转换规则在 XQuery 中 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- XQuery, type casting
- casting rules [XML in SQL Server]
- explicit casting [SQL Server]
- type casting rules [XML in SQL Server]
- cast as operator
- implicit casting
ms.assetid: f2e91306-2b1b-4e1c-b6d8-a34fb9980057
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 31d3c181abbd099f0eec549ead909211e86b0422
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="type-casting-rules-in-xquery"></a>XQuery 中的类型转换规则
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  以下 W3C XQuery 1.0 和 XPath 2.0 函数和运算符规范关系图显示了内置数据类型。 这包括内置基元类型和内置派生类型。  
  
 ![XQuery 1.0 类型层次结构](../xquery/media/xquery-typing-rules.gif "XQuery 1.0 类型层次结构")  
  
 本主题介绍了使用下列方法之一从一种类型转换到另一种类型时所应用的类型转换规则：  
  
-   通过执行显式强制转换，**强制转换为**或类型构造函数 (例如， `xs:integer("5")`)。  
  
-   类型升级过程中发生的隐式转换  
  
## <a name="explicit-casting"></a>显式强制转换  
 下表概括了内置基元类型之间可进行的类型转换。  
  
 ![介绍 XQuery 强制转换规则。](../xquery/media/casting-builtin-types.gif "介绍 XQuery 强制转换规则。")  
  
-   内置基元类型可以根据表中的规则转换为其他内置基元类型。  
  
-   基元类型可以转换为该基元类型所派生的任何类型。 例如，可以强制转换从**xs: decimal**到**xs:integer**，或从**xs: decimal**到**xs:long**。  
  
-   派生类型可以转换为在类型层次结构中作为其祖先的任何类型，最高可转换为其内置基元基类型。 例如，可以强制转换从**xs:token**到**xs:normalizedString**或**xs: string**。  
  
-   如果派生类型的基元祖先可以转换为目标类型，则该派生类型可以转换为基元类型。 例如，你可以强制转换**xs:integer**即为派生类型， **xs: string**、 基元类型，因为**xs: decimal**， **xs:integer**的基元祖先，可以强制转换为**xs: string**。  
  
-   如果源类型的基元祖先可以转换为目标类型的基元祖先，则派生类型可以转换为其他派生类型。 例如，可以强制转换从**xs:integer**到**xs:token**，这是因为你可以从强制转换**xs: decimal**到**xs: string**。  
  
-   将用户定义类型转换为内置类型的规则与转换内置类型的规则相同。 例如，你可以定义**myInteger**类型派生自**xs:integer**类型。 然后， **myInteger**可以强制转换为**xs:token**，这是因为**xs: decimal**可以强制转换为**xs: string**。  
  
 不支持下列类型的转换：  
  
-   不允许转换为列表类型或者由列表类型进行转换。 这包括用户定义的列表类型和内置列表类型如**xs: idrefs**， **xs:ENTITIES**，和**xs:NMTOKENS**。  
  
-   强制转换为或从**xs: qname**不支持。  
  
-   **xs:NOTATION**和持续时间，完全有序子类型**xdt:yearMonthDuration**和**xdt:dayTimeDuration**，不支持。 因此，不支持转换为这些类型或由这些类型转换。  
  
 以下示例说明了显式类型转换。  
  
### <a name="example-a"></a>示例 A  
 以下示例查询 xml 类型的变量。 该查询将返回被类型化为 xs:string 的简单类型值序列。  
  
```  
declare @x xml  
set @x = '<e>1</e><e>2</e>'  
select @x.query('/e[1] cast as xs:string?')  
go  
```  
  
### <a name="example-b"></a>示例 B  
 以下示例查询类型化的 xml 变量。 该示例首先创建 XML 架构集合。 然后使用 XML 架构集合创建类型化的 xml 变量。 该架构为分配给变量的 XML 实例提供了类型化信息。 然后指定对变量进行查询。  
  
```  
create xml schema collection myCollection as N'  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">  
      <xs:element name="root">  
            <xs:complexType>  
                  <xs:sequence>  
                        <xs:element name="A" type="xs:string"/>  
                        <xs:element name="B" type="xs:string"/>  
                        <xs:element name="C" type="xs:string"/>  
                  </xs:sequence>  
            </xs:complexType>  
      </xs:element>  
</xs:schema>'  
go  
```  
  
 因为您不知道文档实例中有多少顶级 <`root`> 元素，所以以下查询将返回一个静态错误。  
  
```  
declare @x xml(myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
          <root><A>4</A><B>5</B><C>6</baz></C>'  
select @x.query('/root/A cast as xs:string?')  
go  
```  
  
 通过在表达式中指定单独的 <`root`> 元素，查询会成功。 该查询将返回被类型化为 xs:string 的简单类型值序列。  
  
```  
declare @x xml(myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
              <root><A>4</A><B>5</B><C>6</C></root>'  
select @x.query('/root[1]/A cast as xs:string?')  
go  
```  
  
 在以下示例中，xml 类型变量包含了指定 XML 架构集合的文档关键字。 这说明 XML 实例必须是具有单个顶级元素的文档。 如果在该 XML 实例中创建两个 <`root`> 元素，则会返回错误。  
  
```  
declare @x xml(document myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
              <root><A>4</A><B>5</B><C>6</C></root>'  
go  
```  
  
 您可以将实例更改为只包含一个顶级元素和查询工作。 查询将再次返回类型化为 xs:string 的简单类型值的序列。  
  
```  
declare @x xml(document myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>'  
select @x.query('/root/A cast as xs:string?')  
go  
```  
  
## <a name="implicit-casting"></a>隐式强制转换  
 只允许对数值类型和 untypedAtomic 类型进行隐式转换。 例如，以下**min （)**函数将返回两个值的最小值：  
  
```  
min(xs:integer("1"), xs:double("1.1"))  
```  
  
 在此示例中，两个值中传递到 XQuery **min （)**函数都是不同的类型。 因此，执行隐式转换其中**整数**类型提升为**double**和第二个**double**值进行比较。  
  
 此示例中介绍的类型升级遵循下列规则：  
  
-   内置派生的数值类型可以升级为其基类型。 例如，**整数**可能被提升为**十进制**。  
  
-   A**十进制**可能被提升为**float、**和**float**可能被提升为**double**。  
  
 因为只允许对数值类型进行隐式转换，所以不允许以下转换：  
  
-   不允许字符串类型的隐式转换。 例如，如果两个**字符串**预期会有类型且你传入**字符串**和**令牌**发生任何隐式强制转换，则返回一个错误。  
  
-   不允许从数值类型隐式转换为字符串类型。 例如，如果将整数类型值传递到需要字符串类型参数的函数，则不发生隐式转换并返回错误。  
  
## <a name="casting-values"></a>强制转换值  
 由一种类型转换为其他类型时，实际值将由源类型的值空间转换为目标类型的值空间。 例如，由 xs:decimal 转换为 xs:double 将把十进制值转换为双精度值。  
  
 下面是一些转换规则。  
  
##### <a name="casting-a-value-from-a-string-or-untypedatomic-type"></a>转换字符串类型的值或 untypedAtomic 类型的值  
 字符串类型或 untypedAtomic 类型的值的转换方式与根据目标类型规则验证值的方式相同。 这包括最终模式规则和空格处理规则。 例如，下例将会成功并生成一个双精度值 1.1e0：  
  
 `xs:double("1.1")`  
  
 如果由字符串类型或 untypedAtomic 类型转换为二进制类型（如 xs:base64Binary 或 xs:hexBinary），则输入值必须分别为 base64 编码形式或 hex 编码形式。  
  
##### <a name="casting-a-value-to-a-string-or-untypedatomic-type"></a>将一个值转换为字符串类型或 untypedAtomic 类型  
 转换为字符串类型或 untypedAtomic 类型会将值转换为其 XQuery 规范词汇表示形式。 确切地说，这表示在输入时遵守特定模式或其他约束的值将不会按照该约束表示。  有关此操作，请通知用户[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]标志其中的类型约束可能会造成问题，这些类型加载到架构集合时提供警告的类型。  
  
 将 xs:float 或 xs:double 类型或者它们任意子类型的值转换为字符串类型或 untypedAtomic 类型的值时，该值将以科学记数法表示。 只有当值的绝对值小于 1.0E-6，或者大于或等于 1.0E6 时才会这样表示。 这表示 0 按科学记数法的形式序列化为 0.0E0。  
  
 例如，`xs:string(1.11e1)` 将返回字符串值 `"11.1"`，而 `xs:string(-0.00000000002e0)` 将返回字符串值 `"-2.0E-11"`。  
  
 如果将二进制类型（如 xs:base64Binary 或 xs:hexBinary）转换为字符串类型或 untypedAtomic 类型，则二进制值将分别以 base64 编码形式或 hex 编码形式表示。  
  
##### <a name="casting-a-value-to-a-numeric-type"></a>将值转换为数值类型  
 如果将一个数值类型的值转换为其他数值类型的值，则该值将从一个值空间映射到另一个值空间，而不会完成字符串序列化。 如果该值不满足目标类型的约束，则应用以下规则：  
  
-   如果资源值已经为数值，且目标类型为允许 -INF 值或 INF 值的 xs:float 类型或其子类型，则转换资源值会导致溢出，并且该值将映射为 INF（如果为正值）或 -INF（如果为负值）。 如果目标类型不允许 INF 或 -INF，则会发生溢出，转换失败且此版本的 SQL Server 中的结果为空序列。  
  
-   如果资源值已经为数值，且目标类型为包含其接受范围内的值 0、-0e0 或 0e0 的数值类型，则转换资源值会导致下溢，并且该值按下列方式映射：  
  
    -   对于 decimal 目标类型，值映射为 0。  
  
    -   当值为下溢负值时，该值映射为 -0e0。  
  
    -   对于 float 目标类型或 double 目标类型，如果值是下溢正值时，该值映射为 0e0。  
  
     如果目标类型在其值空间内不包含零，则转换将失败且结果为空序列。  
  
     请注意，如果将值转换为二进制浮点类型（如 xs:float、xs:double）或它们的任意子类型，可能会丧失精度。  
  
## <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   不支持浮点值 NaN。  
  
-   可转换的值受到目标类型实现限制条件的限制。 例如，不能强制转换为负年份的日期字符串**xs: date**。 如果在运行时提供此值，则这种转换将导致出现空序列（而不是引发运行时错误）。  
  
## <a name="see-also"></a>另请参阅  
 [定义 XML 数据的序列化](../relational-databases/xml/define-the-serialization-of-xml-data.md)  
  
  
