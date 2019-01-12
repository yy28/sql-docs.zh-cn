---
title: XQuery 与静态键入 |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, static typing
- static typing
- checking static types
- inference [XQuery]
ms.assetid: d599c791-200d-46f8-b758-97e761a1a5c0
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 232b071c11d4a2a0bb2e42b6f9787d07f99e21e2
ms.sourcegitcommit: 170c275ece5969ff0c8c413987c4f2062459db21
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2019
ms.locfileid: "54226584"
---
# <a name="xquery-and-static-typing"></a>XQuery 与静态类型化
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 XQuery 是一种静态类型化的语言。 即，在查询编译期间，如果特定函数或运算符不接受表达式返回的值的类型或基数，则会出现类型错误。 此外，静态类型检查还可以检测类型化的 XML 文档的路径表达式是否已正确类型化。 XQuery 编译器首先应用添加隐式运算（例如原子化）的规范化阶段，然后执行静态类型推导和静态类型检查。  
  
## <a name="static-type-inference"></a>静态类型推导  
 静态类型推导用于确定表达式的返回类型。 它通过运用输入参数的静态类型和运算的静态语义并推断结果的静态类型，来确定返回类型。 例如，通过以下方式来确定表达式 1 + 2.3 的静态类型：  
  
-   1 的静态类型是**xs: integer** 2.3 的静态类型是**xs: decimal**。 根据动态语义的静态语义**+** 操作将整数转换为十进制，然后返回一个小数。 推断出的静态类型将是**xs: decimal**。  
  
 对于非类型化的 XML 实例，有一些特殊类型表示数据没有被类型化。 此信息用于静态类型检查期间和执行某些隐式转换。  
  
 对于类型化的数据，输入类型通过约束 XML 数据类型实例的 XML 架构集合来推断。 例如，如果架构允许类型的唯一元素**xs: integer**，使用该元素的路径表达式的结果将是零个或多个类型的元素**xs: integer**。 此结果当前用使用表达式类似于`element(age,xs:integer)*`其中星号 (\*) 指示生成的类型的基数。 在此示例中，表达式可能会导致名为"age"和类型的零个或多个元素**xs: integer**。 其他基数正好是一种，并且必须使用独立的类型名称表示零个或一个，表示使用问号 (**？**)，和 1 或更多和表示通过使用加号 (**+**).  
  
 有时，静态类型推导可以推断出表达式会始终返回空序列。 例如，如果路径表达式在类型化的 XML 数据类型将查找\<名称 > 元素内的\<客户 > 元素 (/ customer/name)，但架构不允许\<名称 > 内\<客户 >，静态类型推导将推断结果将为空。 这将用于检测错误的查询，并且将被视为静态错误，除非表达式为 （） 或**数据 （（））**。  
  
 在 XQuery 规范的正式语义中介绍了详细的推导规则。 Microsoft 对这些规则仅稍加修改，以使用类型化的 XML 数据类型实例。 对该规范所做的最重要的更改是，隐式文档节点了解 XML 数据类型实例的类型。 因此，将根据该信息精确类型化 form /age 的路径表达式。  
  
 通过使用[SQL Server Profiler 模板和权限](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)，可以看到查询编译的一部分返回的静态类型。 若要查看这些静态类型，跟踪必须包括 TSQL 事件类别中的 XQuery 静态类型事件。  
  
## <a name="static-type-checking"></a>静态类型检查  
 静态类型检查用于确保运行时执行仅接收适合该运算的类型的值。 由于无需在运行时检查类型，因此在编译早期可以检测到潜在的错误。 这有助于改善性能。 但是，静态类型化要求查询编写器在表述查询时要更加小心。  
  
 以下为可以使用的适当类型：  
  
-   函数或运算明确允许使用的类型。  
  
-   明确允许使用的类型的子类型。  
  
 子类型是根据使用派生（通过限制或扩展 XML 架构）的子类型化规则定义的。 例如，如果类型为 S 的所有值还是类型 T 的实例，则类型 S 就是类型 T 的子类型。  
  
 此外，根据 XML 架构类型的层次结构，所有整数值还都是小数值。 但是，并非所有小数值都是整数。 因此，整数是小数的子类型，反之则不然。 例如， **+** 操作仅允许某些类型，例如数值类型值**xs: integer**， **xs: decimal**， **xs:float**，并**xs: double**。 如果其他值类型，如**xs: string**，会传递，该操作将引发类型错误。 这称为强类型化。 其他类型（例如用于表示非类型化的 XML 的原子类型）的值可以隐式转换为运算所接受的类型的值。 这称为弱类型化。  
  
 如果要求在隐式转换后进行弱类型化，则静态类型检查可保证只有带有正确基数的允许使用类型的值才会被传递到运算。 对于"string"+ 1，它识别出"string"的静态类型是**xs: string**。 由于这是不允许使用的类型**+** 引发操作，类型错误。  
  
 在将任意表达式 E2 与任意表达式 E1 的结果相加 (E1 + E2) 的情况下，静态类型推导将首先确定 E1 和 E2 的静态类型，然后检查它们的静态类型是否为该运算允许使用的类型。 例如，如果 E1 的静态类型可以是**xs: string**或**xs: integer**、 静态类型检查会发出类型错误、 运行的时即使一些值可能为整数。 相同会出现这种情况，如果 E1 的静态类型**xs: integer&#42;**。 因为**+** 操作只能接受一个整数值和 E1 可能会返回零或大于 1，静态类型检查会发出错误。  
  
 如前面所述，类型推导经常推断出不同于所传递数据的、用户不了解的数据类型。 在这些情况下，用户就必须重写查询。 以下为一些常见的情况：  
  
-   从类型推断出更全面的类型，例如超类型或联合类型。 如果该类型为原子类型，则应该使用转换表达式或构造函数来指明实际的静态类型。 例如，如果表达式 E1 的推断的类型之间进行选择**xs: string**或**xs: integer**而加法要求**xs: integer**，您应编写`xs:integer(E1) + E2`而不是`E1+E2`。 如果遇到字符串值，则此表达式可能会在运行时失败，无法强制转换为**xs: integer**。 但是，这样编写后表达式就可以通过静态类型检查了。 此表达式映射到空序列。  
  
-   从类型推断出比数据实际包含的基数更高的基数。 发生这种情况通常情况下，因为**xml**数据类型可以包含多个顶级元素和 XML 架构集合无法限制此。 为了减少静态类型并保证实际上最多传递一个值，应使用位置谓词 `[1]`。 例如，若要在顶级 a 元素下使元素 `c` 的属性 `b` 的值加 1，则必须编写 `write (/a/b/@c)[1]+1`。 此外，DOCUMENT 关键字可与 XML 架构集合一起使用。  
  
-   某些操作在推导期间会丢失类型信息。 例如，如果无法确定节点的类型，它将成为**anyType**。 这不会隐式转换为任何其他类型。 在使用父轴进行导航期间，尤其会发生这些转换。 如果表达式将产生静态类型错误，则应避免使用这些操作并重写查询。  
  
## <a name="type-checking-of-union-types"></a>联合类型的类型检查  
 由于类型检查，联合类型需要小心处理。 下列示例中说明了其中两个问题。  
  
### <a name="example-function-over-union-type"></a>例如：联合类型的函数  
 例如，以下联合类型的 <`r`> 的元素定义：  
  
```  
<xs:element name="r">  
<xs:simpleType>  
   <xs:union memberTypes="xs:int xs:float xs:double"/>  
</xs:simpleType>  
</xs:element>  
```  
  
 在 XQuery 上下文中，"average"函数`fn:avg (//r)`将返回静态错误，因为 XQuery 编译器无法添加不同类型的值 (**xs: int**， **xs: float**或**xs:双精度**) 的 <`r`> 元素中的参数**fn:avg()**。 若要解决此问题，请将函数调用重写为 `fn:avg(for $r in //r return $r cast as xs:double ?)`。  
  
### <a name="example-operator-over-union-type"></a>例如：联合类型的运算符  
 加法运算（“+”）要求使用精确类型的操作数。 因此，表达式 `(//r)[1] + 1` 将返回静态错误，该错误包含前面所述的 <`r`> 元素的类型定义。 一种解决办法是将其重写为 `(//r)[1] cast as xs:int? +1`，其中“?”表示取 0 或 1 值。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 要求带有“?”的“cast as”，这是因为任何转换都可能由于运行时错误而导致产生空序列。  
  
## <a name="see-also"></a>请参阅  
 [XQuery 语言参考 (SQL Server)](../xquery/xquery-language-reference-sql-server.md)  
  
  
