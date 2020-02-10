---
title: 添加表达式（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a60ee091-b4ed-41e1-9b6a-032c316cd03f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 54505266a77c8baee7f39633ebccd0a5ab5708a8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66106743"
---
# <a name="add-an-expression-report-builder-and-ssrs"></a>添加表达式（报表生成器和 SSRS）
  可在整个报表中使用表达式来定义报表项属性、筛选器、组、排序顺序、连接字符串和参数值。 表达式以等号（=）开头，并且是用编写[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]的。 它们由报表处理器在运行时进行计算，报表处理器会将计算结果和报表布局元素相结合。  
  
 表达式可以是简单的，也可以是复杂的。 简单表达式引用内置集合中的单个项。 复杂表达式可以包括常量、运算符、全局集合项和函数调用。 有关详细信息，请参阅[表达式（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-an-expression-to-a-text-box"></a>向文本框添加表达式  
  
-   在 **“设计”** 视图中，在设计图面上单击要向其添加表达式的文本框。  
  
    -   对于简单表达式，在文本框中键入该表达式的显示文本。 例如，对于数据集字段 Sales，键入 `[Sales]`。  
  
    -   对于复杂表达式，右键单击文本框，然后选择 **“表达式”**。 此时将打开 **“表达式”** 对话框。 在“表达式”窗格中，在等号“=”后键入或交互方式创建表达式，然后单击“确定”。  
  
         该表达式将在设计图面上显示为 `<<Expr>>`。  
  
## <a name="see-also"></a>另请参阅  
 [设置文本和占位符的格式（报表生成器和 SSRS）](formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [文本框（报表生成器和 SSRS）](text-boxes-report-builder-and-ssrs.md)   
 [在报表中使用表达式（报表生成器和 SSRS）](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [筛选器公式示例 &#40;报表生成器和 SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md)   
 [组表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 ["表达式" 对话框 &#40;报表生成器&#41;](../expression-dialog-box-report-builder.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [将代码添加到报表 &#40;SSRS&#41;](add-code-to-a-report-ssrs.md)  
  
  
