---
title: XPath 数据类型 (SQLXML 4.0) |Microsoft Docs
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ff6505dc123405bba8eab3be8bb73bfc4462963c
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43062290"
---
# <a name="xpath-data-types-sqlxml-40"></a>XPath 数据类型 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、XPath 和 XML 架构 (XSD) 具有相差很大的数据类型。 例如，XPath 没有整数或日期数据类型，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 XSD 则具有许多此类数据类型。 XSD 可将纳秒精度用于时间值，而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 最高只能使用 1/300 秒的精度。 因此，将一种数据类型映射到另一种数据类型并不是始终可行的。 有关映射的详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型到 XSD 数据类型，请参阅[数据类型强制转换和 sql: datatype 批注&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)。  
  
 XPath 具有三种数据类型：**字符串**，**数量**，并**布尔**。 **数**数据类型始终是 IEEE 754 双精度浮点。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Float(53)** 数据类型是 XPath 到最接近**数**。 但是， **float(53)** 而言并不是 IEEE 754。 例如，NaN（非数字）和 infinity 均未使用。 尝试将转换为非数值字符串**数**和尝试除以零将导致错误。  
  
## <a name="xpath-conversions"></a>XPath 转换  
 在您使用 `OrderDetail[@UnitPrice > "10.0"]` 之类的 XPath 查询时，隐式和显式数据类型转换可能会对查询的意义产生细微的变化。 因此，理解 XPath 数据类型的实现方式十分重要。 XPath 语言规范，XML 路径语言 (XPath) 版本 1.0 W3C 推荐建议，1999 年 10 月 8，可以在 W3C Web 站点上找到 http://www.w3.org/TR/1999/PR-xpath-19991008.html 。  
  
 XPath 运算符分为四个类别：  
  
-   布尔运算符（and、or）  
  
-   关系运算符 (\<，>， \<=、 > =)  
  
-   相等运算符（=、!=）  
  
-   算术运算符（+、-、*、div、mod）  
  
 每个运算符类别都以不同方式转换其操作数。 XPath 运算符根据需要隐式转换其操作数。 算术运算符将转换为其操作数**数**，并且产生数值。 布尔运算符将对其操作数转换**布尔**，并且产生布尔值。 关系运算符和相等运算符产生布尔值。 但是，根据其操作数的原始数据类型，这两种运算符具有不同的转换规则，如下表所示。  
  
|操作数|关系运算符|相等运算符|  
|-------------|-------------------------|-----------------------|  
|这两种操作数均为节点集。|当且仅当一个节点在一组，并且在第二个节点设置此类，则返回 TRUE，比较其**字符串**值为 TRUE。|相同。|  
|一个是节点集，另**字符串**。|当且仅当在节点集中没有节点，则返回 TRUE，以便在转换为**数量**，它使用的比较**字符串**转换为**数**为 TRUE。|当且仅当在节点集中没有节点，则返回 TRUE，以便在转换为**字符串**，它使用的比较**字符串**为 TRUE。|  
|一个是节点集，另**数**。|当且仅当在节点集中没有节点，则返回 TRUE，以便在转换为**数量**，它使用的比较**数**为 TRUE。|相同。|  
|一个是节点集，另**布尔**。|当且仅当在节点集中没有节点，则返回 TRUE，以便在转换为**布尔**然后**数量**，它使用的比较**布尔**转换为**数**为 TRUE。|当且仅当在节点集中没有节点，则返回 TRUE，以便在转换为**布尔**，它使用的比较**布尔**为 TRUE。|  
|两者均不是节点集。|将转换的两个操作数**数**，然后进行比较。|将两个操作数均转换为常见类型，然后进行比较。 将转换为**布尔**如果有任一项**布尔**，**数**如果有任一项**数**; 否则为将转换为**字符串**.|  
  
> [!NOTE]  
>  因为 XPath 关系运算符始终将转换为其操作数**数量**，**字符串**不可能进行比较。 为了包括日期比较，SQL Server 2000，提供了此向 XPath 规范的变体： 关系运算符比较时**字符串**到**字符串**、 节点集到**字符串**，或字符串值的节点集与字符串的值的节点集，**字符串**比较 (不**数**比较) 执行。  
  
## <a name="node-set-conversions"></a>节点集转换  
 节点集转换并非始终都是直观的。 节点集转换为**字符串**通过集中执行仅第一个节点的字符串值。 节点集转换为**数量**通过将其转换为**字符串**，然后将转换**字符串**到**数**。 节点集转换为**布尔**通过测试其是否存在。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不执行针对节点集的位置选择：例如，XPath 查询 `Customer[3]` 意味着第三个客户；但在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中不支持此类型的位置选择。 因此，节点-设置-到-**字符串**或节点的设置-到-**数**未实现 XPath 规范所述的转换。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用“任何”语义，而 XPath 规范指定“第一个”语义。 例如，基于 W3C XPath 规范，XPath 查询`Order[OrderDetail/@UnitPrice > 10.0]`的第一个选择以下顺序**OrderDetail**具有**UnitPrice**大于 10.0。 在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此 XPath 查询选择以下任何顺序**OrderDetail**具有**UnitPrice**大于 10.0。  
  
 转换为**布尔**产生存在测试; 因此，XPath 查询`Products[@Discontinued=true()]`等效于 SQL 表达式"Products.Discontinued is not null"，非 SQL 表达式"Products.Discontinued = 1"。 若要使查询等效于后者的 SQL 表达式，第一次节点-将该集转换为非**布尔**类型，如**数**。 例如 `Products[number(@Discontinued) = true()]` 。  
  
 因为如果运算符对于节点集中任一节点为 TRUE，则大多数运算符均定义为 TRUE；所以，在节点集为空时，这些运算的计算结果始终为 FALSE。 因此，如果 A 为空，则 `A = B` 和 `A != B` 均为 FALSE，并且 `not(A=B)` 和 `not(A!=B)` 均为 TRUE。  
  
 通常情况下，某个属性或元素映射到的列存在不在数据库中的列的值是否**null**。 如果元素的任何子集存在，则映射到行的元素将存在。  
  
> [!NOTE]  
>  元素使用批注**是常量**始终存在。 因此，不能用于 XPath 谓词**是常量**元素。  
  
 当节点集转换为**字符串**或**数**、 带批注的架构中检查其 XDR 类型 （如果有） 和该类型用于确定是必需的转换。  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>将 XDR 数据类型映射到 XPath 数据类型  
 节点的 XPath 数据类型派生从 XDR 数据类型在架构中下, 表中所示 (节点**EmployeeID**用于演示目的)。  
  
|XDR 数据类型|等效<br /><br /> XPath 数据类型|使用的 SQL Server 转换|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|N/A|NoneEmployeeID|  
|boolean|boolean|CONVERT(bit, EmployeeID)|  
|number、int、float、i1、i2、i4、i8、r4、r8、ui1、ui2、ui4、ui8|number|CONVERT(float(53), EmployeeID)|  
|id、idref、idrefsentity、entities、enumerationnotation、nmtoken、nmtokens、chardate、Timedate、Time.tz、string、uri、uuid|string|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|无（在 XPath 中没有等效于 fixed14.4 XDR 数据类型的数据类型）|CONVERT(money, EmployeeID)|  
|日期|string|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|string|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 日期和时间转换旨在用于使用在数据库中存储的值是否[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime**数据类型或**字符串**。 请注意， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime**数据类型不使用**时区**并且具有比 XML 更低的精度**时间**数据类型。 若要包括**时区**数据类型或附加的精度，存储中的数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用**字符串**类型。  
  
 在某一节点从其 XDR 数据类型转换为 XPath 数据类型时，有时候可能需要执行附加的转换（从一个 XPath 数据类型转换为另一个 XPath 数据类型）。 例如，请考虑下面的 XPath 查询：  
  
```  
(@m + 3) = 4  
```  
  
 如果@m属于**fixed14.4** XDR 数据类型到 XPath 数据类型通过从 XDR 数据类型转换：  
  
```  
CONVERT(money, m)  
```  
  
 在此转换中，节点`m`转换从**fixed14.4**到**资金**。 但如果添加值 3，则要求附加的转换：  
  
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
 在根据带批注的 XSD 架构指定的以下 XPath 查询，该查询用于选择所有**员工**具有节点**EmployeeID**属性值为 E-1，其中"E-"是使用指定的前缀**sql:id-前缀**批注。  
  
 `Employee[@EmployeeID="E-1"]`  
  
 该查询中的谓词等效于 SQL 表达式：  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 因为**EmployeeID**是之一**id** (**idref**， **idrefs**， **nmtoken**， **nmtokens**，依次类推) 数据类型值在 XSD 架构中， **EmployeeID**转换为**字符串**使用前述转换规则的 XPath 数据类型。  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 “E-”前缀将添加到字符串，然后结果将与 `N'E-1'` 进行比较。  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. 在 XPath 查询中执行若干数据类型转换  
 考虑以下根据带批注的 XSD 架构指定的 XPath 查询：`OrderDetail[@UnitPrice * @OrderQty > 98]`  
  
 此 XPath 查询返回所有 **\<OrderDetail >** 满足谓词的元素`@UnitPrice * @OrderQty > 98`。 如果**UnitPrice**使用批注**fixed14.4**带批注的架构中的数据类型是此谓词等效于 SQL 表达式：  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 在 XPath 查询中转换值时，第一个转换将 XDR 数据类型转换为 XPath 数据类型。 因为 XSD 数据类型的**UnitPrice**是**fixed14.4**上, 一个表中所述，这是使用第一个转换：  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 因为算术运算符将转换为其操作数**数量**XPath 数据类型，第二个转换 （从另一个 XPath 数据类型到一个 XPath 数据类型） 应用在其中的值转换为**float(53)** (**float(53)** 类似于 XPath**数**数据类型):  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 假设**OrderQty**属性具有任何 XSD 数据类型**OrderQty**转换为**数**单个转换中的 XPath 数据类型：  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 同样，值 98 将转换到**数**XPath 数据类型：  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  如果在该架构中使用的 XSD 数据类型与数据库中的基础 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型不兼容，或者不可能执行 XPath 数据类型转换，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能会返回错误。 例如，如果**EmployeeID**属性将批注**id 前缀**批注，XPath`Employee[@EmployeeID=1]`生成一个错误，因为**EmployeeID**具有**id 前缀**批注并且不能转换为**数**。  
  
  
