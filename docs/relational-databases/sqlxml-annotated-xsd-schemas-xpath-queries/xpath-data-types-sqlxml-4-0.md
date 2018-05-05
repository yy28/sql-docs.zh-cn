---
title: XPath 数据类型 (SQLXML 4.0) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
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
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7762ba02f4368b64fc4073936cb04c293029e9d2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="xpath-data-types-sqlxml-40"></a>XPath 数据类型 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、XPath 和 XML 架构 (XSD) 具有相差很大的数据类型。 例如，XPath 没有整数或日期数据类型，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 XSD 则具有许多此类数据类型。 XSD 可将纳秒精度用于时间值，而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 最高只能使用 1/300 秒的精度。 因此，将一种数据类型映射到另一种数据类型并不是始终可行的。 有关映射的详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型与 XSD 数据类型，请参阅[数据类型强制和 sql: datatype 批注&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)。  
  
 XPath 有三种数据类型：**字符串**，**数**，和**布尔**。 **数**数据类型始终是 IEEE 754 双精度浮点。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Float(53)** 数据类型是最接近 XPath**数**。 但是， **float(53)** IEEE 754 预览并不完全。 例如，NaN（非数字）和 infinity 均未使用。 尝试将转换到非数字字符串**数**和尝试除以零会产生错误。  
  
## <a name="xpath-conversions"></a>XPath 转换  
 在您使用 `OrderDetail[@UnitPrice > "10.0"]` 之类的 XPath 查询时，隐式和显式数据类型转换可能会对查询的意义产生细微的变化。 因此，理解 XPath 数据类型的实现方式十分重要。 XPath 语言规范中，XML 路径语言 (XPath) 版本 1.0 W3C 建议建议 1999 年 10 月 8，可以在 W3C Web 站点找到http://www.w3.org/TR/1999/PR-xpath-19991008.html。  
  
 XPath 运算符分为四个类别：  
  
-   布尔运算符（and、or）  
  
-   关系运算符 (\<，>， \<=、 > =)  
  
-   相等运算符（=、!=）  
  
-   算术运算符（+、-、*、div、mod）  
  
 每个运算符类别都以不同方式转换其操作数。 XPath 运算符根据需要隐式转换其操作数。 算术运算符将转换为其操作数**数**，并且一个数字值将导致。 布尔运算符转换为其操作数**布尔**，并且将导致一个布尔值。 关系运算符和相等运算符产生布尔值。 但是，根据其操作数的原始数据类型，这两种运算符具有不同的转换规则，如下表所示。  
  
|操作数|关系运算符|相等运算符|  
|-------------|-------------------------|-----------------------|  
|这两种操作数均为节点集。|当且仅当一组中必须有一个节点且第二个中的节点集如 TRUE 该比较其**字符串**值为 TRUE。|相同。|  
|其中一个是节点集，另**字符串**。|当且仅当存在中节点集是一个节点，则返回 TRUE 以便时转换为**数**，它使用的比较**字符串**转换为**数**为 TRUE。|当且仅当存在中节点集是一个节点，则返回 TRUE，以便当转换为**字符串**，它使用的比较**字符串**为 TRUE。|  
|其中一个是节点集，另**数**。|当且仅当存在中节点集是一个节点，则返回 TRUE 以便时转换为**数**，它使用的比较**数**为 TRUE。|相同。|  
|其中一个是节点集，另**布尔**。|当且仅当存在中节点集是一个节点，则返回 TRUE 以便时转换为**布尔**然后**数**，它使用的比较**布尔**转换为**数**为 TRUE。|当且仅当存在中节点集是一个节点，则返回 TRUE，以便当转换为**布尔**，它使用的比较**布尔**为 TRUE。|  
|两者均不是节点集。|将转换的两个操作数**数**，然后进行比较。|将两个操作数均转换为常见类型，然后进行比较。 将转换为**布尔**如果存在任何一种**布尔**，**数**如果存在任何一种**数**; 否则为将转换为**字符串**.|  
  
> [!NOTE]  
>  因为 XPath 关系运算符始终转换为其操作数**数**，**字符串**比较都不可能。 若要包含日期比较，SQL Server 2000 提供 XPath 规范此变体： 当关系运算符比较**字符串**到**字符串**、 节点设置为**字符串**，或一个字符串值节点的设置为字符串值节点集，**字符串**比较 (不**数**比较) 执行。  
  
## <a name="node-set-conversions"></a>节点集转换  
 节点集转换并非始终都是直观的。 节点集转换为**字符串**采用集中只有第一个节点的字符串值。 节点集转换为**数**通过将其转换为**字符串**，然后将转换**字符串**到**数**。 节点集转换为**布尔**通过测试其是否存在。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不执行针对节点集的位置选择：例如，XPath 查询 `Customer[3]` 意味着第三个客户；但在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中不支持此类型的位置选择。 因此，节点的设置-到-**字符串**或节点的设置-到-**数**未实现由 XPath 规范所述的转换。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用“任何”语义，而 XPath 规范指定“第一个”语义。 例如，基于 W3C XPath 规范，XPath 查询`Order[OrderDetail/@UnitPrice > 10.0]`与第一个选择这些订单**OrderDetail**具有**UnitPrice**大于 10.0。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此 XPath 查询选择与任意这些订单**OrderDetail**具有**UnitPrice**大于 10.0。  
  
 转换为**布尔**生成是否存在测试; 因此，XPath 查询`Products[@Discontinued=true()]`等效于 SQL 表达式"Products.Discontinued is not null"，不是 SQL 表达式"Products.Discontinued = 1"。 若要使查询等效于后一种 SQL 表达式，第一次节点-将该集转换为非**布尔**类型，如**数**。 例如， `Products[number(@Discontinued) = true()]`。  
  
 因为如果运算符对于节点集中任一节点为 TRUE，则大多数运算符均定义为 TRUE；所以，在节点集为空时，这些运算的计算结果始终为 FALSE。 因此，如果 A 为空，则 `A = B` 和 `A != B` 均为 FALSE，并且 `not(A=B)` 和 `not(A!=B)` 均为 TRUE。  
  
 通常情况下，某个属性或元素映射到某一列存在如果该数据库中的列的值不是**null**。 如果元素的任何子集存在，则映射到行的元素将存在。  
  
> [!NOTE]  
>  使用批注元素**是常量**始终存在。 因此，XPath 谓词不能用于**是常量**元素。  
  
 当节点集转换为**字符串**或**数**、 已批注的架构中检查其 XDR 类型 （如果有） 和该类型用于确定是必需的转换。  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>将 XDR 数据类型映射到 XPath 数据类型  
 节点的 XPath 数据类型派生自 XDR 数据类型在架构中下, 表中所示 (节点**EmployeeID**用于说明目的)。  
  
|XDR 数据类型|等效<br /><br /> XPath 数据类型|使用的 SQL Server 转换|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|N/A|NoneEmployeeID|  
|boolean|boolean|CONVERT(bit, EmployeeID)|  
|number、int、float、i1、i2、i4、i8、r4、r8、ui1、ui2、ui4、ui8|number|CONVERT(float(53), EmployeeID)|  
|id、idref、idrefsentity、entities、enumerationnotation、nmtoken、nmtokens、chardate、Timedate、Time.tz、string、uri、uuid|string|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|无（在 XPath 中没有等效于 fixed14.4 XDR 数据类型的数据类型）|CONVERT(money, EmployeeID)|  
|date|string|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|string|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 日期和时间转换被设计用于是否值存储在数据库中使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime**数据类型或**字符串**。 请注意， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime**数据类型不使用**时区**和具有比 XML 较小的精度**时间**数据类型。 若要包括**时区**数据类型或其他精度，存储中的数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用**字符串**类型。  
  
 在某一节点从其 XDR 数据类型转换为 XPath 数据类型时，有时候可能需要执行附加的转换（从一个 XPath 数据类型转换为另一个 XPath 数据类型）。 例如，请考虑下面的 XPath 查询：  
  
```  
(@m + 3) = 4  
```  
  
 如果@m的**fixed14.4** XDR 数据类型，与 XPath 数据类型通过从 XDR 数据类型转换：  
  
```  
CONVERT(money, m)  
```  
  
 在此转换中，节点`m`转换从**fixed14.4**到**money**。 但如果添加值 3，则要求附加的转换：  
  
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
||X 未知|X 是**字符串**|X 是**数**|X 是**布尔**|  
|string(X)|CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
|number(X)|CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
|boolean(X)|-|LEN(X) > 0|X != 0|-|  
  
## <a name="examples"></a>示例  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>A. 在 XPath 查询中转换数据类型  
 在以下 XPath 查询中指定对带批注的 XSD 架构，查询将选择所有**员工**节点与**EmployeeID**属性的 E-1，其中"E-"是使用指定的前缀值**sql:id-前缀**批注。  
  
 `Employee[@EmployeeID="E-1"]`  
  
 该查询中的谓词等效于 SQL 表达式：  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 因为**EmployeeID**是之一**id** (**idref**， **idrefs**， **nmtoken**， **nmtokens**，依次类推) 数据在 XSD 架构中，键入值**EmployeeID**转换为**字符串**使用前面所述的转换规则的 XPath 数据类型。  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 “E-”前缀将添加到字符串，然后结果将与 `N'E-1'` 进行比较。  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. 在 XPath 查询中执行若干数据类型转换  
 考虑以下根据带批注的 XSD 架构指定的 XPath 查询：`OrderDetail[@UnitPrice * @OrderQty > 98]`  
  
 此 XPath 查询返回所有 **\<OrderDetail >** 满足谓词的元素`@UnitPrice * @OrderQty > 98`。 如果**UnitPrice**使用批注**fixed14.4**数据类型中批注的架构，此谓词相当于 SQL 表达式：  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 在 XPath 查询中转换值时，第一个转换将 XDR 数据类型转换为 XPath 数据类型。 因为 XSD 数据类型的**UnitPrice**是**fixed14.4**，如在上表中所述，这是使用第一次转换：  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 因为算术运算符转换为其操作数**数**XPath 数据类型，第二个 （从一个 XPath 数据类型设置为另一个 XPath 数据类型） 换算为在其中的值转换为**float(53)** (**float(53)** 接近 XPath**数**数据类型):  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 假设**OrderQty**属性具有任何 XSD 数据类型， **OrderQty**转换为**数**中单个转换的 XPath 数据类型：  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 同样，98 的值转换为**数**XPath 数据类型：  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  如果在该架构中使用的 XSD 数据类型与数据库中的基础 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型不兼容，或者不可能执行 XPath 数据类型转换，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能会返回错误。 例如，如果**EmployeeID**属性进行批注**id 前缀**批注，XPath`Employee[@EmployeeID=1]`生成错误，因为**EmployeeID**具有**id 前缀**批注而不能转换为**数**。  
  
  
