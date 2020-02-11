---
title: 设置文本框方向（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 64bd53f4-2f31-4732-8c2e-64c7b54b6972
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6acffc286e913d35846b2eeb156cf1980b42fab3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66104981"
---
# <a name="set-text-box-orientation-report-builder-and-ssrs"></a>设置文本框方向（报表生成器和 SSRS）
  文本框可以有不同的方向：水平、垂直（从上到下读取文本）或旋转 270 度（从下到上读取文本）。 由于是对文本框而非文本设置方向，因此方向适用于文本框中的所有文本。 不能为文本的各个部分指定不同的方向。 需手动调整列宽和行高的大小以容纳旋转的文本。  
  
 用于指定文本方向的 WritingMode 属性在 "**文本框属性**" 对话框中不可用。 您需要打开“属性”窗格并且在该窗格中设置属性。 WritingMode 属性的可用值为 "**水平**" （从左向右文本）、"**垂直**" （从上到下的文本阅读）、" **Rotate270** " （从下到上的文本读取）。 必须手动调整列宽和行高的大小以容纳文本。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-text-orientation"></a>设置文本方向  
  
1.  创建一个新报表或打开现有报表。  
  
2.  如果“属性”窗格未打开，请单击 **“视图”** 选项卡并选中 **“属性”** 复选框。  
  
3.  单击要更改文本方向的文本框。  
  
4.  在 "属性" 窗格中找到 "WritingMode" 属性，然后在下拉列表中选择要应用到文本框的文本方向。  
  
    > [!NOTE]  
    >  对“属性”窗格中的属性进行分类时，WritingMode 位于“本地化”类别中  。  
  
5.  在列表框中，选择 **Horizontal**、 **Vertical**或 **Rotate270**。  
  
## <a name="see-also"></a>另请参阅  
 [文本框（报表生成器和 SSRS）](text-boxes-report-builder-and-ssrs.md)   
 [教程：设置文本格式（报表生成器）](../tutorial-format-text-report-builder.md)  
  
  
