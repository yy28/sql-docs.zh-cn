---
title: 表达式中的运算符（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d22dc8b6-4353-40e7-91a1-65e8dae6325d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4499e62cf8564705b96ec74d2598c311e0097709
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47817095"
---
# <a name="operators-in-expressions-report-builder-and-ssrs"></a>表达式中的运算符（报表生成器和 SSRS）
  运算符是一种符号，用来表示要应用到表达式中一个或多个字词的操作。 表达式中支持下列类别的运算符：算术、比较、串联、逻辑或位，以及移位。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="arithmetic"></a>算术  
 算术运算符对表达式中的两个数值字词执行数学运算。  
  
|运算符|描述|  
|--------------|-----------------|  
|^|以一个数字为底、另一数字为幂求值。|  
|*|使两个数字相乘。|  
|/|使两个数字相除，返回浮点结果。|  
|\|使两个数字相除，返回整数结果。|  
|Mod|返回一个除法运算的整数余数。 例如，7 Mod 5 = 2，这是因为 7 除以 5，余数为 2。|  
|+|将两个数相加。|  
|-|返回两个数字之差或表示一个数值字词的负值。|  
  
### <a name="comparison"></a>比较  
 比较运算符测试两个表达式是否相同。  
  
|运算符|描述|  
|--------------|-----------------|  
|<|小于。|  
|\<=|小于等于。|  
|>|大于。|  
|>=|大于等于。|  
|=|等于。|  
|<>|不等于。|  
|Like|确定特定字符串是否与指定模式相匹配。 模式可以包含常规字符和通配符。 模式匹配过程中，常规字符必须与字符串中指定的字符完全匹配。 但是，通配符可以与字符串的任意部分相匹配。 与使用 = 和 != 字符串比较运算符相比，使用通配符可使 LIKE 运算符更加灵活。<br /><br /> 下表列出了可以用作通配符的字符：<br /><br /> %：包含零个或多个字符的任意字符串。<br /><br /> _：任何单个字符。<br /><br /> [ ]：指定范围（例如 [a-f]）或集合（例如 [aeiou]）内的任何单个字符。<br /><br /> [^]：不在指定范围（例如 [^a - f]）或集合（例如 [^aeiou]）内的任何单个字符|  
|Is|比较两个对象引用。|  
  
### <a name="string-concatenation"></a>字符串串联  
 字符串串联将第二个字符串追加到表达式中的第一个字符串。 对于其他字符串运算，使用内置函数。  
  
|运算符|描述|  
|--------------|-----------------|  
|&|串联两个字符串|  
|+|串联两个字符串|  
  
### <a name="logical-and-bitwise"></a>逻辑和位  
 逻辑运算符和位运算符在表达式中的两个整数字词之间执行逻辑操作。  
  
|运算符|描述|  
|--------------|-----------------|  
|And|对两个布尔表达式执行逻辑与运算，或对两个数值表达式执行位与运算。|  
|Not|对布尔表达式执行逻辑非运算，或对数值表达式执行位求反运算。|  
|或|对两个布尔表达式执行逻辑或运算，或对两个数值执行位或运算。|  
|Xor|对两个布尔表达式执行逻辑异运算，或对两个数值表达式执行位异运算。|  
|AndAlso|对两个表达式执行逻辑与运算。|  
|OrElse|对两个表达式执行逻辑或运算。|  
  
### <a name="bit-shift"></a>移位  
 位运算符在表达式中的两个整数字词之间执行位操作。  
  
|运算符|描述|  
|--------------|-----------------|  
|<\<|对位模式执行算术左移位运算。|  
|>>|对位模式执行算术右移位运算。|  
  
## <a name="see-also"></a>另请参阅  
 [“表达式”对话框](http://msdn.microsoft.com/library/e6c74ccb-4594-4d4f-b958-618d710e34eb)   
 [表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [“表达式”对话框（报表生成器）](http://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)  
  
  
