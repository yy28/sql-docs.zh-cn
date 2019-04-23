---
title: 设置文本框方向（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 64bd53f4-2f31-4732-8c2e-64c7b54b6972
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 08f25381a87074720868b68c8c095dd8b2136d59
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59956653"
---
# <a name="set-text-box-orientation-report-builder-and-ssrs"></a>设置文本框方向（报表生成器和 SSRS）
  文本框可以有不同的方向：水平、垂直（从上到下读取文本）或旋转 270 度（从下到上读取文本）。 由于是对文本框而非文本设置方向，因此方向适用于文本框中的所有文本。 不能为文本的各个部分指定不同的方向。 需手动调整列宽和行高的大小以容纳旋转的文本。  
  
 用于指定文本方向的 WritingMode 属性不是在可用**文本框属性**对话框。 您需要打开“属性”窗格并且在该窗格中设置属性。 可用值为 WritingMode 属性**水平**（读取的文本从左到右），**垂直**（文本从上到下读取） 和**Rotate270** （读取的文本从下到上）。 必须手动调整列宽和行高的大小以容纳文本。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-set-text-orientation"></a>设置文本方向  
  
1.  创建一个新报表或打开现有报表。  
  
2.  如果“属性”窗格未打开，请单击 **“视图”** 选项卡并选中 **“属性”** 复选框。  
  
3.  单击要更改文本方向的文本框。  
  
4.  找到 WritingMode 属性，在属性窗格中，并在下拉列表中选择要应用到文本框中的文本方向。  
  
    > [!NOTE]  
    >  对“属性”窗格中的属性进行分类时，WritingMode 位于“本地化”类别中。  
  
5.  在列表框中，选择 **Horizontal**、 **Vertical**或 **Rotate270**。  
  
## <a name="see-also"></a>请参阅  
 [文本框（报表生成器和 SSRS）](text-boxes-report-builder-and-ssrs.md)   
 [教程：设置文本格式（报表生成器）](../tutorial-format-text-report-builder.md)  
  
  
