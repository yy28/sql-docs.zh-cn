---
title: 表达式中的常量（报表生成器）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: b8ae650b-0f46-4848-b62b-15f8a40751b8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0231c41e3104756232c55cb4c4707948605a35e6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "77077071"
---
# <a name="constants-in-expressions-report-builder-and-ssrs"></a>表达式中的常量（报表生成器和 SSRS）
  常量由文字文本或预定义文本构成。 报表处理器具有对预定义常量的访问权限，所以当表达式中包含常量时，这些常量所代表的值会在计算之前进行替换。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="literal-text"></a>文字文本  
 在表达式中，文字文本是用双引号括起来的文本。 如果文本不是表达式的一部分，也可以在文本框中直接键入文本，而不使用双引号。 如果文本框值不以等号 (=) 开头，则会将该文本视为文字文本。 下表显示几个表达式中的文字文本示例。  
  
|一直|显示文本|表达式文本|  
|--------------|------------------|---------------------|  
|Report run at:|<\<Expr>>|`="Report run at: " & Globals!ExecutionTime`|  
|Adventure Works Cycles|Adventure Works Cycles|Adventure Works Cycles|  
|[Bracketed display text]|\\[Bracketed display text\\]|[Bracketed display text]|  
  
## <a name="rdl-constants"></a>RDL 常量  
 您可以在表达式中使用以报表定义语言 (RDL) 定义的常量。 在 **“表达式”** 对话框中，当创建只接受某些有效值（也称为枚举类型）的报表属性的表达式时，显示常量。 下表显示两个示例。  
  
|properties|说明|值|  
|--------------|-----------------|------------|  
|TextAlign|文本框中对齐文本的有效值。|General、Left、Center、Right|  
|BorderStyle|添加到报表的行的有效值。|Default、None、Dotted、Dashed、Solid、Double、DashDot、DashDotdot|  
  
## <a name="visual-basic-constants"></a>Visual Basic 常量  
 您可以在表达式中使用在 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 运行时库定义的常量。 例如，可以使用常量 **DateInterval.Day**。 对于日期 2008 年 1 月 10 日，以下表达式会返回数字 10：  
  
 `=DatePart("d",Globals!ExecutionTime)`  
  
## <a name="clr-constants"></a>CLR 常量  
 可以在表达式中使用在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 公共语言运行时 (CLR) 类中定义的常量。 下表显示了系统定义的颜色的一个示例。  
  
|一直|说明|  
|--------------|-----------------|  
|MistyRose|创建基于背景色的报表属性的表达式时，可以按名称指定颜色。 **“表达式”** 对话框中列出了有效名称。|  
  
## <a name="see-also"></a>另请参阅  
 [“表达式”对话框](https://msdn.microsoft.com/library/e6c74ccb-4594-4d4f-b958-618d710e34eb)   
 [表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [“表达式”对话框（报表生成器）](https://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)  
  
  
