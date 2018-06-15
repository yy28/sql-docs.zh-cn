---
title: 设置文本框方向（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 64bd53f4-2f31-4732-8c2e-64c7b54b6972
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bf2588b4e5c958a15eefd0c8745489005799a842
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33023654"
---
# <a name="set-text-box-orientation-report-builder-and-ssrs"></a>设置文本框方向（报表生成器和 SSRS）
在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分页报表中，可对文本框进行不同方向的旋转：   
* 水平旋转   
* 垂直旋转（旋转 90 度，从上到下阅读的文本）  
* 旋转 270 度（从下到上阅读的文本）。   
  
由于旋转的是文本框而非文本，因此旋转适用于文本框中的所有文本。 不能为文本的各个部分指定不同的方向。 需手动调整列宽和行高的大小以容纳旋转的文本。  
  
 用于指定文本方向的 WritingMode 属性不在“文本框属性”对话框中。 它在“属性”窗格中，并在此设置属性。   
  
## <a name="to-rotate-text"></a>旋转文本  
  
1.  创建报表或打开现有报表，并向设计图面 [添加文本框](../../reporting-services/report-design/add-move-or-delete-a-text-box-report-builder-and-ssrs.md) 。  
  
3.  选择要旋转的文本框。  
  
2.  如果“属性”窗格未打开，请在“视图”选项卡上选中“属性”复选框。  
  
4.  在“属性”窗格中查找 WritingMode 属性，选择要应用到文本框的文本方向。  
  
    > [!NOTE]  
    >  对“属性”窗格中的属性进行分类时，WritingMode 位于“本地化”类别中。  
  
5.  在列表框中，选择 **Horizontal**、 **Vertical**或 **Rotate270**。  
  
## <a name="see-also"></a>另请参阅  
 [文本框（报表生成器和 SSRS）](../../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)   
 [教程：设置文本格式（报表生成器）](../../reporting-services/tutorial-format-text-report-builder.md)  
  
  
