---
title: 错误处理 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- static errors
- errors [XQuery]
- XQuery, error handling
- dynamic errors [XQuery]
ms.assetid: 7dee3c11-aea0-4d10-9126-d54db19448f2
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 444fa51144535475f67cc0d073b63cb1b8354531
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687278"
---
# <a name="error-handling-xquery"></a>错误处理 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  W3C 规范允许静态或动态引发类型错误，并定义了静态错误、动态错误和类型错误。  
  
## <a name="compilation-and-error-handling"></a>编译和错误处理  
 语法不正确的 Xquery 表达式和 XML DML 语句会返回编译错误。 编译阶段会检查 XQuery 表达式和 DML 语句的静态类型正确性，并针对类型化的 XML 使用 XML 架构进行类型推理。 如果表达式在运行时由于类型安全冲突而失败，会引起静态类型错误。 静态错误的示例包括将字符串添加到整数，以及在不存在的节点中查询类型化的数据。  
  
 与 W3C 标准有所不同的是，XQuery 运行时错误被转换为空序列。 这些序列根据调用上下文，可以作为空 XML 或 NULL 传播到查询结果。  
  
 通过显式转换为正确的类型，用户可以解决静态错误的问题，尽管运行时转换错误将被转换为空序列。  
  
## <a name="static-errors"></a>静态错误  
 静态错误是通过使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 错误机制返回的。 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，XQuery 类型错误是静态返回的。 有关详细信息，请参阅[XQuery 与静态类型化](../xquery/xquery-and-static-typing.md)。  
  
## <a name="dynamic-errors"></a>动态错误  
 在 XQuery 中，大部分动态错误都映射到一个空序列（即“()”）。 不过，有两个例外：XQuery 聚合函数中的溢出条件和 XML-DML 验证错误。 请注意，大部分动态错误都映射到一个空序列。 另外，使用 XML 索引的查询执行可能引发错误。 因此，为了能够有效地执行索引而不生成意外错误，[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]会将动态错误映射到 ()。  
  
 通常，在谓词内出现动态错误的情况下，不引发错误就不会更改语义，因为 () 映射到 False。 但是，在某些情况下，返回 () 而不返回动态错误可能导致意外结果。 下列示例说明了这一点。  
  
### <a name="example-using-the-avg-function-with-a-string"></a>示例：使用带字符串的 avg() 函数  
 在以下示例中， [avg 函数](../xquery/aggregate-functions-avg.md)称为计算的三个值的平均值。 这些值中的一个是字符串。 由于此情况下的 XML 实例是非类型化的，因此其中的所有数据都是非类型化的原子类型。 **Avg （)** 函数首先将转换这些值与**xs: double**计算平均值之前。 但是，值`"Hello"`，不能强制转换为**xs: double**和生成动态错误。 在这种情况下，而不是返回动态错误的强制转换`"Hello"`到**xs: double**会导致空序列。 **Avg （)** 函数将忽略此值，计算另两个值的平均值，并返回 150。  
  
```  
DECLARE @x xml  
SET @x=N'<root xmlns:myNS="test">  
 <a>100</a>  
 <b>200</b>  
 <c>Hello</c>  
</root>'  
SELECT @x.query('avg(//*)')  
```  
  
### <a name="example-using-the-not-function"></a>示例：使用 not 函数  
 当你使用[不起作用](../xquery/functions-on-boolean-values-not-function.md)在谓词中，例如， `/SomeNode[not(Expression)]`，并且该表达式会导致动态错误，一个空序列将返回而不是错误。 将应用**not （)** 到空序列，则返回 True，而不是错误。  
  
### <a name="example-casting-a-string"></a>示例：转换字符串  
 在下面的示例中，文字字符串“NaN”先转换为 xs:string，再转换为 xs:double。 结果是一个空行集。 虽然字符串“NaN”无法成功转换为 xs:double，但直到运行时才能确定，因为该字符串首先转换为 xs:string。  
  
```  
DECLARE @x XML  
SET @x = ''  
SELECT @x.query(' xs:double(xs:string("NaN")) ')  
GO  
```  
  
 不过，在此示例中，生成一个静态类型错误。  
  
```  
DECLARE @x XML  
SET @x = ''  
SELECT @x.query(' xs:double("NaN") ')  
GO  
```  
  
#### <a name="implementation-limitations"></a>实现限制  
 **Fn:error()** 不支持函数。  
  
## <a name="see-also"></a>请参阅  
 [XQuery 语言参考 (SQL Server)](../xquery/xquery-language-reference-sql-server.md)   
 [XQuery 基础知识](../xquery/xquery-basics.md)  
  
  
