---
title: XPath 数据类型 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 3e4a0c3d8b7a01f43b03d3f94b48d5bba800b64f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014559"
---
# <a name="xpath-data-types-sqlxml-40"></a>XPath 数据类型 (SQLXML 4.0)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、XPath 和 XML 架构 (XSD) 具有相差很大的数据类型。 例如，XPath 没有整数或日期数据类型，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 XSD 则具有许多此类数据类型。 XSD 可将纳秒精度用于时间值，而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 最高只能使用 1/300 秒的精度。 因此，将一种数据类型映射到另一种数据类型并不是始终可行的。 有关映射的详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型到 XSD 数据类型，请参阅[数据类型强制转换和 sql: datatype 批注&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)。  
  
 XPath 具有三种数据类型：`string`、`number` 和 `boolean`。 `number` 数据类型始终是 IEEE 754 双精度浮点。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `float(53)`数据类型是 XPath 到最接近`number`。 但是，`float(53)` 与 IEEE 754 并不完全相同。 例如，NaN（非数字）和 infinity 均未使用。 尝试将非数字字符串转换为 `number` 和尝试以零作除数将导致错误。  
  
## <a name="xpath-conversions"></a>XPath 转换  
 在您使用 `OrderDetail[@UnitPrice > "10.0"]` 之类的 XPath 查询时，隐式和显式数据类型转换可能会对查询的意义产生细微的变化。 因此，理解 XPath 数据类型的实现方式十分重要。 XPath 语言规范，XML 路径语言 (XPath) 版本 1.0 W3C 推荐建议，1999 年 10 月 8，可以在 W3C Web 站点上找到 http://www.w3.org/TR/1999/PR-xpath-19991008.html 。  
  
 XPath 运算符分为四个类别：  
  
-   布尔运算符（and、or）  
  
-   关系运算符 (\<，>， \<=、 > =)  
  
-   相等运算符（=、!=）  
  
-   算术运算符（+、-、*、div、mod）  
  
 每个运算符类别都以不同方式转换其操作数。 XPath 运算符根据需要隐式转换其操作数。 算术运算符将其操作数转换为 `number`，并且产生数值。 布尔运算符将其操作数转换为 `boolean`，并且产生布尔值。 关系运算符和相等运算符产生布尔值。 但是，根据其操作数的原始数据类型，这两种运算符具有不同的转换规则，如下表所示。  
  
|操作数|关系运算符|相等运算符|  
|-------------|-------------------------|-----------------------|  
|这两种操作数均为节点集。|当且仅当在一个集合中存在某一节点并且在第二个集合中存在某一节点时为 TRUE，这样，其 `string` 值的比较为 TRUE。|相同。|  
|一个是节点集，另一个是 `string`。|当且仅当在该节点集中存在某一节点时为 TRUE，这样在转换为 `number` 时，它与转换为 `string` 的 `number` 的比较为 TRUE。|当且仅当在该节点集中存在某一节点时为 TRUE，这样在转换为 `string` 时，它与 `string` 的比较为 TRUE。|  
|一个是节点集，另一个是 `number`。|当且仅当在该节点集中存在某一节点时为 TRUE，这样在转换为 `number` 时，它与 `number` 的比较为 TRUE。|相同。|  
|一个是节点集，另一个是 `boolean`。|当且仅当在该节点集中存在某一节点时为 TRUE，这样在转换为 `boolean` 然后转换为 `number` 时，它与转换为 `boolean` 的 `number` 的比较为 TRUE。|当且仅当在该节点集中存在某一节点时为 TRUE，这样在转换为 `boolean` 时，它与 `boolean` 的比较为 TRUE。|  
|两者均不是节点集。|将两个操作数均转换为 `number`，然后进行比较。|将两个操作数均转换为常见类型，然后进行比较。 转换为 `boolean`（如果其中一个是 `boolean`）或转换为 `number`（如果其中一个是 `number`）；否则，转换为 `string`。|  
  
> [!NOTE]  
>  因为 XPath 关系运算符始终将其操作数转换为 `number`，所以，不可能执行 `string` 比较。 为了包括日期比较，SQL Server 2000 提供了此向 XPath 规范的变体：关系运算符比较时`string`到`string`、 节点设置为`string`，或字符串值的节点集与字符串的值的节点集，`string`比较 (不`number`比较) 执行。  
  
## <a name="node-set-conversions"></a>节点集转换  
 节点集转换并非始终都是直观的。 一个节点集通过只取该节点集中第一个节点的字符串值，转换为 `string`。 通过将某一节点集转换为 `number`，然后将 `string` 转换为 `string`，将该节点集转换为 `number`。 节点集将通过测试其是否存在，转换为 `boolean`。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不执行针对节点集的位置选择：例如，XPath 查询 `Customer[3]` 意味着第三个客户；但在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中不支持此类型的位置选择。 因此，无法实现 XPath 规范所述的节点集到 `string` 转换或者节点集到 `number` 转换。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用“任何”语义，而 XPath 规范指定“第一个”语义。 例如，基于 W3C XPath 规范，XPath 查询`Order[OrderDetail/@UnitPrice > 10.0]`的第一个选择以下顺序**OrderDetail**具有**UnitPrice**大于 10.0。 在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此 XPath 查询选择以下任何顺序**OrderDetail**具有**UnitPrice**大于 10.0。  
  
 转换为 `boolean` 将产生存在测试；因此，XPath 查询 `Products[@Discontinued=true()]` 等效于 SQL 表达式“Products.Discontinued is not null”，而非 SQL 表达式“Products.Discontinued = 1”。 若要使该查询等效于后一个 SQL 表达式，请首先将节点集转换为非 `boolean` 类型，如 `number`。 例如， `Products[number(@Discontinued) = true()]` 。  
  
 因为如果运算符对于节点集中任一节点为 TRUE，则大多数运算符均定义为 TRUE；所以，在节点集为空时，这些运算的计算结果始终为 FALSE。 因此，如果 A 为空，则 `A = B` 和 `A != B` 均为 FALSE，并且 `not(A=B)` 和 `not(A!=B)` 均为 TRUE。  
  
 通常，如果数据库中某一列的值不是 `null`，则映射到该列的属性或元素将存在。 如果元素的任何子集存在，则映射到行的元素将存在。  
  
> [!NOTE]  
>  使用 `is-constant` 批注的元素始终存在。 因此，XPath 谓词不能用于 `is-constant` 元素。  
  
 在某一节点集转换为 `string` 或 `number` 时，在带批注的架构中检查其 XDR 类型（如果有）并且该类型用于确定该转换是否是必需的。  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>将 XDR 数据类型映射到 XPath 数据类型  
 节点的 XPath 数据类型派生从 XDR 数据类型在架构中下, 表中所示 (节点**EmployeeID**用于演示目的)。  
  
|XDR 数据类型|等效<br /><br /> XPath 数据类型|使用的 SQL Server 转换|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|不可用|NoneEmployeeID|  
|boolean|boolean|CONVERT(bit, EmployeeID)|  
|number、int、float、i1、i2、i4、i8、r4、r8、ui1、ui2、ui4、ui8|number|CONVERT(float(53), EmployeeID)|  
|id、idref、idrefsentity、entities、enumerationnotation、nmtoken、nmtokens、chardate、Timedate、Time.tz、string、uri、uuid|string|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|无（在 XPath 中没有等效于 fixed14.4 XDR 数据类型的数据类型）|CONVERT(money, EmployeeID)|  
|date|string|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|string|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 日期和时间转换旨在用于使用在数据库中存储的值是否[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]`datetime`数据类型或`string`。 请注意， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `datetime`数据类型不使用`timezone`并且具有比 XML 更低的精度`time`数据类型。 若要包括 `timezone` 数据类型或附加的精度，请使用 `string` 类型在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中存储数据。  
  
 在某一节点从其 XDR 数据类型转换为 XPath 数据类型时，有时候可能需要执行附加的转换（从一个 XPath 数据类型转换为另一个 XPath 数据类型）。 例如，请考虑下面的 XPath 查询：  
  
```  
(@m + 3) = 4  
```  
  
 如果@m属于`fixed14.4`XDR 数据类型到 XPath 数据类型通过从 XDR 数据类型转换：  
  
```  
CONVERT(money, m)  
```  
  
 在此转换中，节点 `m` 从 `fixed14.4` 转换到 `money`。 但如果添加值 3，则要求附加的转换：  
  
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
||X 未知|X 是 `string`|X 是 `number`|X 是 `boolean`|  
|string(X)|CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
|number(X)|CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
|boolean(X)|-|LEN(X) > 0|X != 0|-|  
  
## <a name="examples"></a>示例  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>A. 在 XPath 查询中转换数据类型  
 在根据带批注的 XSD 架构指定的以下 XPath 查询，该查询用于选择所有**员工**具有节点**EmployeeID**属性值为 E-1，其中"E-"是使用指定的前缀`sql:id-prefix`批注。  
  
 `Employee[@EmployeeID="E-1"]`  
  
 该查询中的谓词等效于 SQL 表达式：  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 因为**EmployeeID**是之一`id`(`idref`， `idrefs`， `nmtoken`，`nmtokens`等) 数据类型值在 XSD 架构中， **EmployeeID**是转换为`string`使用前述转换规则的 XPath 数据类型。  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 “E-”前缀将添加到字符串，然后结果将与 `N'E-1'` 进行比较。  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. 在 XPath 查询中执行若干数据类型转换  
 考虑以下根据带批注的 XSD 架构指定的 XPath 查询：`OrderDetail[@UnitPrice * @OrderQty > 98]`  
  
 此 XPath 查询返回所有 **\<OrderDetail >** 满足谓词的元素`@UnitPrice * @OrderQty > 98`。 如果**UnitPrice**使用批注`fixed14.4`带批注的架构中的数据类型是此谓词等效于 SQL 表达式：  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 在 XPath 查询中转换值时，第一个转换将 XDR 数据类型转换为 XPath 数据类型。 因为 XSD 数据类型的**UnitPrice**是`fixed14.4`上, 一个表中所述，这是使用第一个转换：  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 因为算术运算符将其操作数转换为 `number` XPath 数据类型，所以，第二个转换（从一个 XPath 数据类型到另一个 XPath 数据类型）将应用于其值转换为 `float(53)` 的情况（`float(53)` 类似于 XPath `number` 数据类型）：  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 假设**OrderQty**属性具有任何 XSD 数据类型**OrderQty**转换为`number`单个转换中的 XPath 数据类型：  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 与此类似，值 98 将转换为 `number` XPath 数据类型：  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  如果在该架构中使用的 XSD 数据类型与数据库中的基础 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型不兼容，或者不可能执行 XPath 数据类型转换，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能会返回错误。 例如，如果**EmployeeID**属性将批注`id-prefix`批注，XPath`Employee[@EmployeeID=1]`生成一个错误，因为**EmployeeID**具有`id-prefix`批注并不能转换为`number`。  
  
  
