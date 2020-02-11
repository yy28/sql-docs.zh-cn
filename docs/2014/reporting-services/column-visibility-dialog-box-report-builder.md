---
title: "\"列可见性\" 对话框（报表生成器） |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10127"
ms.assetid: 0c030cab-6087-45a5-99f0-c7bd693f20a1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 58381a9e56ed6ace1f8ff18109d9746072f76774
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109808"
---
# <a name="column-visibility-dialog-box-report-builder"></a>“列可见性”对话框（报表生成器）
  在报表首次运行时使用 **“列可见性”** 对话框来显示或隐藏选中的列，其他时候可通过此对话框使用另一报表项来切换该列的可见性。  
  
## <a name="options"></a>选项  
 **在报表最初运行时**  
 选择一个选项以指示报表项在报表中的初始显示方式。  
  
 **显示**  
 选择此选项可显示列。  
  
 **隐藏**  
 选择此选项可隐藏列。  
  
 **基于表达式显示或隐藏**  
 选择此选项可以使初始可见性根据表达式相应变化。  
  
 键入计算结果为 `Boolean` 值的表达式，值为 `True` 时表示隐藏该项，值为 `False` 时表示显示该项。 单击 "表达式" （*fx*）按钮可编辑表达式。  
  
 **可以通过此报表项切换显示**  
 选择此选项可以显示一个切换图像，用户可以使用该图像在 HTML 报表查看器中显示或隐藏此列。  
  
 您需要键入或选择报表中要用来显示切换图像的文本框的名称；例如，Textbox1。 所选择的文本框必须在此报表项的当前或包含作用域中。 例如，若要切换与子组关联的行的可见性，请在与父组关联的行中选择一个文本框。 若要切换图表的可见性，请选择一个与该图表位于同一包含作用域中的文本框；例如，表体或矩形。  
  
## <a name="see-also"></a>另请参阅  
 [表达式示例（报表生成器和 SSRS）](report-design/expression-examples-report-builder-and-ssrs.md)   
 [向项 &#40;报表生成器和 SSRS 添加展开或折叠操作&#41;](report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [图像（报表生成器和 SSRS）](report-design/images-report-builder-and-ssrs.md)   
 [报表生成器对话框、窗格和向导的帮助](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [“图像属性”对话框 ->“常规”（报表生成器和 SSRS）](../../2014/reporting-services/image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
