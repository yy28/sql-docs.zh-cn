---
title: XPath 数据类型 （SQLXML）
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping XDR types to XPath types [SQLXML]
- data types [XPath]
- arithmetic operators
- mapping data types [SQLXML]
- relational operators [SQLXML]
- node-set [SQLXML]
- data types [SQLXML], XPath
- XPath operators [SQLXML]
- XDR data type [SQLXML]
- equality operators [SQLXML]
- XPath conversions [SQLXML]
- converting data types [SQLXML]
- Boolean operators
- XPath queries [SQLXML], data types
- XPath data types [SQLXML]
- operators [SQLXML]
ms.assetid: a90374bf-406f-4384-ba81-59478017db68
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 089b2b006d0159c63e480c8627762ac37dec98b8
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2020
ms.locfileid: "75247090"
---
# <a name="xpath-data-types-sqlxml-40"></a>XPath 数据类型 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，XPath 和 XML 架构 （XSD） 的数据类型非常不同。 例如，XPath 没有整数或日期数据类型，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 XSD 则具有许多此类数据类型。 XSD 可将纳秒精度用于时间值，而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 最高只能使用 1/300 秒的精度。 因此，将一种数据类型映射到另一种数据类型并不是始终可行的。 有关将数据类型映射到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]XSD 数据类型的详细信息，请参阅[数据类型强制和 sql：数据类型注释&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)。  
  
 XPath 有三种数据类型：**字符串**、**数字**和**布尔。** **数字**数据类型始终为 IEEE 754 双精度浮点。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**浮点（53）** 数据类型最接近 XPath**编号**。 但是，**浮点 （53）** 不完全是 IEEE 754。 例如，NaN（非数字）和 infinity 均未使用。 尝试将非数字字符串转换为**数字**并尝试除以零会导致错误。  
  
## <a name="xpath-conversions"></a>XPath 转换  
 在您使用 `OrderDetail[@UnitPrice > "10.0"]` 之类的 XPath 查询时，隐式和显式数据类型转换可能会对查询的意义产生细微的变化。 因此，理解 XPath 数据类型的实现方式十分重要。 XPath 语言规范，XML 路径语言 （XPath） 版本 1.0 W3C 建议 1999 年 10 月http://www.w3.org/TR/1999/PR-xpath-19991008.html8 日，可在 W3C 网站找到。  
  
 XPath 运算符分为四个类别：  
  
-   布尔运算符（and、or）  
  
-   关系运算符（、>、*、>\< \<*）  
  
-   相等运算符（=、!=）  
  
-   算术运算符（+、-、*、div、mod）  
  
 每个运算符类别都以不同方式转换其操作数。 XPath 运算符根据需要隐式转换其操作数。 算术运算符将其操作数转换为**数字**，并产生数字值。 布尔运算符将其操作数转换为**布尔，** 并产生布尔值。 关系运算符和相等运算符产生布尔值。 但是，根据其操作数的原始数据类型，这两种运算符具有不同的转换规则，如下表所示。  
  
|操作数|关系运算符|相等运算符|  
|-------------|-------------------------|-----------------------|  
|这两种操作数均为节点集。|如果仅在一个集中有一个节点和第二个集中有一个节点，以便比较其**字符串**值为 TRUE 时，才具有 TRUE。|相同。|  
|一个是节点集，另一个是**字符串**。|TRUE，如果并且仅当节点集中有一个节点，这样当转换为**数字**时，它与转换为**数字**的**字符串**的比较才为 TRUE。|TRUE，如果并且仅当节点集中有一个节点，因此当转换为**字符串**时，它与**字符串**的比较是 TRUE。|  
|一个是节点集，另一个是**数字**。|TRUE，如果并且仅当节点集中有一个节点，这样当转换为**数字**时，它与**数字**的比较才为 TRUE。|相同。|  
|一个是节点集，另一个是**布尔。**|TRUE，如果并且仅当节点集中有一个节点，这样当转换为**布尔**，然后转换为**数字**时，它与转换为**数字**的**布尔**的比较才为 TRUE。|TRUE，如果并且仅当节点集中有一个节点，这样当转换为**布尔**时，它与**布尔**的比较才是真实的。|  
|两者均不是节点集。|将两个操作数转换为**数字**，然后进行比较。|将两个操作数均转换为常见类型，然后进行比较。 如果任一是布尔，则转换为布尔，如果任**一数字为**"布尔 **"，****则为 "布尔";** 如果任一数字，则为**布尔**。否则，转换为**字符串**。|  
  
> [!NOTE]  
>  由于 XPath 关系运算符始终将其操作数转换为**数字**，因此无法进行**字符串**比较。 为了包括日期比较，SQL Server 2000 提供了与 XPath 规范的此变体：当关系运算符将**字符串**与**字符串**进行比较时，将节点集与**字符串**进行比较，或者将字符串值节点集与字符串值节点集进行比较，则执行**字符串**比较（而不是**数字**比较）。  
  
## <a name="node-set-conversions"></a>节点集转换  
 节点集转换并非始终都是直观的。 节点集通过仅获取集中第一个节点的字符串值转换为**字符串**。 节点集通过将其转换为**字符串**，然后将**字符串**转换为数字，将其转换为**数字**。 **number** 节点集通过测试其存在转换为**布尔。**  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不执行针对节点集的位置选择：例如，XPath 查询 `Customer[3]` 意味着第三个客户；但在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中不支持此类型的位置选择。 因此，不实现 XPath 规范描述的节点集到**字符串**或节点集到**数**转换。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用“任何”语义，而 XPath 规范指定“第一个”语义。 例如，基于 W3C XPath 规范，XPath 查询`Order[OrderDetail/@UnitPrice > 10.0]`选择具有**单价**大于 10.0 的第一**个订单详细信息**的订单。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，此 XPath 查询选择具有**单价**大于 10.0 的任何**订单详细信息**的订单。  
  
 转换为**布尔**生成存在测试;因此，XPath 查询`Products[@Discontinued=true()]`等效于 SQL 表达式"产品.已停产不是空"，而不是 SQL 表达式"产品.已停产 = 1"。 要使查询等效于后者 SQL 表达式，请先将节点集转换为非**布尔**类型，如**数字**。 例如，`Products[number(@Discontinued) = true()]` 。  
  
 因为如果运算符对于节点集中任一节点为 TRUE，则大多数运算符均定义为 TRUE；所以，在节点集为空时，这些运算的计算结果始终为 FALSE。 因此，如果 A 为空，则 `A = B` 和 `A != B` 均为 FALSE，并且 `not(A=B)` 和 `not(A!=B)` 均为 TRUE。  
  
 通常，如果数据库中该列的值不**为空**，则存在映射到列的属性或元素。 如果元素的任何子集存在，则映射到行的元素将存在。  
  
> [!NOTE]  
>  带有**正常量**的带号表示的元素始终存在。 因此，XPath 谓词不能用于**常量**元素。  
  
 当节点集转换为**字符串**或**数字**时，其 XDR 类型（如果有）在批带的架构中检查，该类型用于确定所需的转换。  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>将 XDR 数据类型映射到 XPath 数据类型  
 节点的 XPath 数据类型派生自架构中的 XDR 数据类型，如下表所示（节点**EmployID**用于说明目的）。  
  
|XDR 数据类型|等效<br /><br /> XPath 数据类型|使用的 SQL Server 转换|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|空值|NoneEmployeeID|  
|boolean|boolean|CONVERT(bit, EmployeeID)|  
|number、int、float、i1、i2、i4、i8、r4、r8、ui1、ui2、ui4、ui8|数字|CONVERT(float(53), EmployeeID)|  
|id、idref、idrefsentity、entities、enumerationnotation、nmtoken、nmtokens、chardate、Timedate、Time.tz、string、uri、uuid|字符串|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|无（在 XPath 中没有等效于 fixed14.4 XDR 数据类型的数据类型）|CONVERT(money, EmployeeID)|  
|date|字符串|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|字符串|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 日期和时间转换旨在处理该值是否使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**日期时间**数据类型或**字符串**存储在数据库中。 请注意，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**日期时间**数据类型不使用**时区**，其精度比 XML**时间**数据类型小。 要包括**时区**数据类型或其他精度，请使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**字符串**类型将数据存储在其中。  
  
 在某一节点从其 XDR 数据类型转换为 XPath 数据类型时，有时候可能需要执行附加的转换（从一个 XPath 数据类型转换为另一个 XPath 数据类型）。 例如，请考虑下面的 XPath 查询：  
  
```  
(@m + 3) = 4  
```  
  
 如果是@m**固定 14.4** XDR 数据类型，则使用以下途径完成从 XDR 数据类型转换为 XPath 数据类型的转换：  
  
```  
CONVERT(money, m)  
```  
  
 在此转换中，节点`m`从固定**14.4**转换为**货币**。 但如果添加值 3，则要求附加的转换：  
  
```  
CONVERT(float(CONVERT(money, m))  
```  
  
 该 XPath 表达式计算为：  
  
```  
CONVERT(float(CONVERT(money, m)) + CONVERT(float(53), 3) = CONVERT(float(53), 3)  
```  
  
 如下表中所示，这一转换同样适用于其他 XPath 表达式（例如文字表达式或复合表达式）。  
  
||||||  
|-|-|-|-|-|  
||X 未知|X 是**字符串**|X 是**数字**|X 是**布尔**|  
|string(X)|CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
|number(X)|CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
|boolean(X)|-|LEN（X） > 0|X != 0|-|  
  
## <a name="examples"></a>示例  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>A. 在 XPath 查询中转换数据类型  
 在以下针对带注释的 XSD 架构指定的 XPath 查询中，该查询选择所有**员工**节点，其员工**ID**属性值为 E-1，其中"E-"是使用**sql：id 前缀**注释指定的前缀。  
  
 `Employee[@EmployeeID="E-1"]`  
  
 该查询中的谓词等效于 SQL 表达式：  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 由于**EmployID**是 XSD 架构中的**id**id（idref、idrefs、nmtoken、nmtokens 等）数据类型值之一，因此使用前面描述的转换规则将**idrefs****Employid**转换为**字符串**XPath 数据类型。**idref** **nmtoken** **nmtokens**  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 “E-”前缀将添加到字符串，然后结果将与 `N'E-1'` 进行比较。  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. 在 XPath 查询中执行若干数据类型转换  
 考虑以下根据带批注的 XSD 架构指定的 XPath 查询：`OrderDetail[@UnitPrice * @OrderQty > 98]`  
  
 此 XPath 查询返回满足谓词`@UnitPrice * @OrderQty > 98`的所有**\<Order 详细信息>** 元素。 如果在注释的架构中用**固定 14.4**数据类型注释**UnitPrice，** 则此谓词等效于 SQL 表达式：  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 在 XPath 查询中转换值时，第一个转换将 XDR 数据类型转换为 XPath 数据类型。 由于**UnitPrice**的 XSD 数据类型是固定的**14.4**，如上表中所述，这是使用的第一个转换：  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 由于算术运算符将其操作数转换为**数字**XPath 数据类型，因此应用第二次转换（从一个 XPath 数据类型转换为另一个 XPath 数据类型），其中将值转换为**float（53）** **（float（53）** 接近 XPath**数字**数据类型）：  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 假设**OrderQty**属性没有 XSD 数据类型，**则 OrderQty**在单个转换中转换为**数字**XPath 数据类型：  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 同样，值 98 将转换为**数字**XPath 数据类型：  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  如果在该架构中使用的 XSD 数据类型与数据库中的基础 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型不兼容，或者不可能执行 XPath 数据类型转换，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能会返回错误。 例如，如果**EmployID**属性使用**id 前缀**注释进行批注，则`Employee[@EmployeeID=1]`XPath 将生成错误，因为**EmployID**具有**id 前缀**注释，无法转换为**数字**。  
  
  
