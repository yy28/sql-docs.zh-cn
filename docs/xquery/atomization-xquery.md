---
title: "原子化 (XQuery) |Microsoft 文档"
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: XML
helpviewer_keywords:
- XQuery, atomization
- atomization [XQuery]
ms.assetid: e3d7cf2f-c6fb-43c2-8538-4470a6375af5
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b6be2574663ce5b8f2cb51161033799543f4ca2e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="atomization-xquery"></a>原子化 (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  原子化是提取项的类型化值的过程。 在某些环境下，此进程是隐式进行的。 某些 XQuery 运算符（如算术运算符和比较运算符）依赖于此进程。 例如，当你算术运算符将直接应用于节点，则节点的类型化的值第一次检索通过隐式调用[数据函数](../xquery/data-accessor-functions-data-xquery.md)。 这将把原子值作为操作数传递给算术运算符。  
  
 例如，下面的查询将返回 LaborHours 属性的总数。 在这种情况下， **data （)**隐式应用于属性节点。  
  
```  
declare @x xml  
set @x='<ROOT><Location LID="1" SetupTime="1.1" LaborHours="3.3" />  
<Location LID="2" SetupTime="1.0" LaborHours="5" />  
<Location LID="3" SetupTime="2.1" LaborHours="4" />  
</ROOT>'  
-- data() implicitly applied to the attribute node sequence.  
SELECT @x.query('sum(/ROOT/Location/@LaborHours)')  
```  
  
 尽管没有要求，你也可以显式指定**data （)**函数：  
  
```  
SELECT @x.query('sum(data(ROOT/Location/@LaborHours))')  
```  
  
 隐式原子化的另一个示例是使用算术运算符。 **+** 运算符要求原子值，和**data （)**隐式应用检索 LaborHours 属性的原子值。 针对 Instructions 列指定的查询**xml** ProductModel 表中的类型。 下面的查询将返回 LaborHours 属性三次。 在该查询中，请注意下列情况：  
  
-   构造 OrignialLaborHours 属性时，原子化隐式应用于 `$WC/@LaborHours` 返回的单独序列。 LaborHours 属性的类型化值被分配给 OrignialLaborHours。  
  
-   在构造 UpdatedLaborHoursV1 属性时，算术运算符需要原子值。 因此， **data （)**隐式应用于返回的 LaborHours 属性 (`$WC/@LaborHours`)。 然后，原子值 1 添加到该属性。 构造的属性 UpdatedLaborHoursV2 演示的显式应用**data （)**，但不是必需的。  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location[1]  
        return  
            <WC OriginalLaborHours = "{ $WC/@LaborHours }"  
                UpdatedLaborHoursV1 = "{ $WC/@LaborHours + 1 }"   
                UpdatedLaborHoursV2 = "{ data($WC/@LaborHours) + 1 }" >  
            </WC>') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 结果如下：  
  
```  
<WC OriginalLaborHours="2.5"   
    UpdatedLaborHoursV1="3.5"   
    UpdatedLaborHoursV2="3.5" />  
```  
  
 原子化将导致简单类型、空集、静态类型的实例错误。  
  
 原子化还会发生在比较表达式参数传递给函数，函数，返回值**cast()**表达式和排序表达式按顺序传递 by 子句。  
  
## <a name="see-also"></a>另请参阅  
 [XQuery 基础知识](../xquery/xquery-basics.md)   
 [比较表达式 &#40;XQuery &#41;](../xquery/comparison-expressions-xquery.md)   
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
