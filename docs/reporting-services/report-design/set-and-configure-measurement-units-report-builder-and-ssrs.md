---
title: 设置和配置度量单位（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: a15a96c3-7d2c-433e-a440-4ea051e967a9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 48700208f4ff67c9f6b6932537558c283df13ee6
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "65576648"
---
# <a name="set-and-configure-measurement-units-report-builder-and-ssrs"></a>设置和配置度量单位（报表生成器和 SSRS）
  在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分页报表中，指示器使用以下两个度量单位之一：百分比或数值。   
    
  默认情况下，指示器配置为使用百分比作为度量单位。 这意味着分配给指示器集中各图标的指示器值由百分比范围确定。 百分比范围在指示器集中的各图标上平均划分。 每个图标都表示一个指示器状态。 您可以通过指定不同的开始和结束百分比，更改指示器集中每个图标的百分比。 指示器还自动检测数据中的最小值和最大值。  
  
 您可以将度量单位更改为数值。 在此情况下，不要为数据指定最小值或最大值；而是为指示器使用的每个图标仅提供开始值和结束值。  
  
 可以通过使用表达式设置度量单位之类的选项。 有关详细信息，请参阅[表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)。  
  
## <a name="to-use-the-numeric-state-measurement-unit"></a>使用数字状态度量单位  
  
1.  右键单击要更改的指示器，然后单击“指示器属性”。  
  
2.  在左窗格中单击 **“值和状态”** 。  
  
3.  在 **“状态度量单位”** 列表中，单击 **“数字”**。  
  
     或者，单击“表达式”(fx) 按钮，编辑设置该选项的值的表达式。  
  
4.  对于指示器集中的每个图标，在 **“开始”** 和 **“结束”** 文本框中更新值。  
  
     或者，单击“表达式”(fx) 按钮，编辑设置“开始”和“结束”选项的值的表达式。  
  
    > [!NOTE]  
    >  “开始”和“结束”文本框中的值必须是数字。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-use-the-percentage-measurement-unit"></a>使用百分比度量单位  
  
1.  右键单击要更改的指示器，然后单击“指示器属性”。  
  
2.  在左窗格中单击 **“值和状态”** 。  
  
3.  在 **“状态度量单位”** 列表中，单击 **“百分比”**。  
  
     或者，单击“表达式”(fx) 按钮，编辑设置该选项的值的表达式。  
  
4.  还可以更改 **“最小值”** 和 **“最大值”** 选项以使用特定值，而非自动检测指示器使用的数据的最小值和最大值。 **“最小值”** 必须小于 **“最大值”**。  
  
    > [!NOTE]  
    >  如果您显式设置最小值和最大值，则指示器将使用该值范围，而与数据中的实际最小值和最大值无关。 这意味着，在确定要在报表中显示的指示器图标的计算中，将排除低于最小值的值和高于最大值的值。  
  
     或者，单击“表达式”(fx) 按钮，编辑设置该选项的值的表达式。  
  
5.  对于指示器集中的每个图标，在 **“开始”** 和 **“结束”** 文本框中更新值。  
  
     或者，单击“表达式”(fx) 按钮，编辑设置“开始”和“结束”选项的值的表达式。  
  
    > [!NOTE]  
    >  “开始”和“结束”文本框中的值必须是数字。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [指示器（报表生成器和 SSRS）](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
