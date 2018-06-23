---
title: 行可见性对话框 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rtp.rptdesigner.rowvisibility.f1
- "10126"
ms.assetid: 557ecf70-62b1-47f5-9322-0ebdc809d018
caps.latest.revision: 12
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 8bcc02cc0e210bf2cbd7ee974ba5d2057658dfe7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125056"
---
# <a name="row-visibility-dialog-box"></a>“行可见性”对话框
  在报表首次运行时可使用 **“行可见性”** 对话框来显示或隐藏选中的行，其他时候可通过此对话框使用另一报表项来切换该行的可见性。  
  
## <a name="options"></a>“常规”  
 **在报表最初运行时**  
 选择一个选项以指示报表项在报表中的初始显示方式。  
  
 **显示**  
 选择此选项以显示报表项。  
  
 **隐藏**  
 选择此选项以隐藏报表项。  
  
 **显示或隐藏基于表达式**  
 选择此选项可以利用表达式来使初始可见性具有可变性。  
  
 键入一个表达式，计算结果为`Boolean`值`True`可以隐藏项和`False`表示显示该项。 单击“表达式”(**fx**) 按钮可编辑表达式。  
  
 **可以通过此报表项切换显示**  
 选择此选项可以显示一个切换图像，用户可以使用该图像在 HTML 报表查看器中显示或隐藏此报表项。  
  
 您需要键入或选择报表中要用来显示切换图像的文本框的名称；例如，Textbox1。 所选择的文本框必须在此报表项的当前或包含作用域中。 例如，若要切换与子组关联的行的可见性，请在与父组关联的行中选择一个文本框。 若要切换图表的可见性，请选择一个与该图表位于同一包含作用域中的文本框；例如，表体或矩形。  
  
## <a name="see-also"></a>请参阅  
 [表达式示例（报表生成器和 SSRS）](report-design/expression-examples-report-builder-and-ssrs.md)   
 [为项添加展开或折叠操作（报表生成器和 SSRS）](report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [映像&#40;报表生成器和 SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [报表设计器的 F1 帮助](tools/report-designer-f1-help.md)  
  
  