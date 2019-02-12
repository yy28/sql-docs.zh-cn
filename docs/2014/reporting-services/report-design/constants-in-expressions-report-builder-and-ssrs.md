---
title: 表达式中的常量（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: b8ae650b-0f46-4848-b62b-15f8a40751b8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ae4079f0f7be0bb854a8c77737251fdfd09ca0b6
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56035488"
---
# <a name="constants-in-expressions-report-builder-and-ssrs"></a>表达式中的常量（报表生成器和 SSRS）
  常量由文字文本或预定义文本构成。 报表处理器具有对预定义常量的访问权限，所以当表达式中包含常量时，这些常量所代表的值会在计算之前进行替换。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="literal-text"></a>文字文本  
 在表达式中，文字文本是用双引号括起来的文本。 如果文本不是表达式的一部分，也可以在文本框中直接键入文本，而不使用双引号。 如果文本框值不以等号 (=) 开头，则会将该文本视为文字文本。 下表显示几个表达式中的文字文本示例。  
  
|常量|显示文本|表达式文本|  
|--------------|------------------|---------------------|  
|Report run at:|<\<Expr>>|`="Report run at: " & Globals!ExecutionTime`|  
|Adventure Works Cycles|Adventure Works Cycles|Adventure Works Cycles|  
|[Bracketed display text]|\\[Bracketed display text\\]|[Bracketed display text]|  
  
## <a name="rdl-constants"></a>RDL 常量  
 您可以在表达式中使用以报表定义语言 (RDL) 定义的常量。 在 **“表达式”** 对话框中，当创建只接受某些有效值（也称为枚举类型）的报表属性的表达式时，显示常量。 下表显示两个示例。  
  
|属性|Description|值|  
|--------------|-----------------|------------|  
|TextAlign|文本框中对齐文本的有效值。|General、Left、Center、Right|  
|BorderStyle|添加到报表的行的有效值。|Default、None、Dotted、Dashed、Solid、Double、DashDot、DashDotdot|  
  
## <a name="visual-basic-constants"></a>Visual Basic 常量  
 您可以在表达式中使用在 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 运行时库定义的常量。 例如，可以使用常量 `DateInterval.Day`。 对于日期 2008 年 1 月 10 日，以下表达式会返回数字 10：  
  
 `=DatePart("d",Globals!ExecutionTime)`  
  
## <a name="clr-constants"></a>CLR 常量  
 可以在表达式中使用在 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 公共语言运行时 (CLR) 类中定义的常量。 下表显示了系统定义的颜色的一个示例。  
  
|常量|Description|  
|--------------|-----------------|  
|MistyRose|创建基于背景色的报表属性的表达式时，可以按名称指定颜色。 **“表达式”** 对话框中列出了有效名称。|  
  
## <a name="see-also"></a>请参阅  
 [“表达式”对话框](../expression-dialog-box.md)   
 [表达式（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](data-types-in-expressions-report-builder-and-ssrs.md)   
 [“表达式”对话框（报表生成器）](../expression-dialog-box-report-builder.md)  
  
  
