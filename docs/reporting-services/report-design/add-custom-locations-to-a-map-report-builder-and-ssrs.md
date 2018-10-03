---
title: 向地图添加自定义位置（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- MICROSOFT.REPORTDESIGNER.MAPPOINT.POINTTEMPLATE
ms.assetid: 7d36faae-5bcc-446a-9eba-f42349cafacb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5b3ab32ed1e5924a38b35bc2ad6664a23ff712a3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724601"
---
# <a name="add-custom-locations-to-a-map-report-builder-and-ssrs"></a>向地图添加自定义位置（报表生成器和 SSRS）
  向 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分页报表添加地图之后，可以添加你自己的点位置。  
  
 通过设置层的点属性的选项来控制层上所有点的显示属性。 对于所选的嵌入点，可以覆盖这些显示属性。  
  
> [!NOTE]  
>  覆盖该嵌入点的层显示属性时，您所做的更改无法还原。  
  
 有关详细信息，请参阅 [按规则和分析数据更改多边形、线条和点的显示方式（报表生成器和 SSRS）](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-add-a-point-layer"></a>添加点层  
  
1.  在报表设计图面中，单击该地图以选择它并显示“地图”窗格。  
  
2.  在工具栏中，单击 **“添加层”**。  
  
3.  从下拉列表中，单击“添加点层”。 将不包含点的点层添加到该地图。 默认情况下，为嵌入的点准备了点层。  
  
## <a name="to-add-a-custom-point"></a>添加自定义点  
  
1.  在报表设计图面中，单击该地图以选择它并显示“地图”窗格。  
  
2.  在“地图”窗格中，右键单击具有类型“嵌入”的点层，然后单击“添加点”。 光标将变为十字准线。  
  
3.  若要添加点，请单击地图上的某个位置。 在您单击的位置将嵌入的点添加到所选层中。  
  
## <a name="to-customize-the-display-for-an-embedded-point"></a>自定义嵌入点的显示方式  
  
1.  右键单击该点，然后单击“点属性”。 将打开 **“地图嵌入点属性”** 对话框。  
  
2.  单击 **“覆盖此层的点选项”**。 将在左窗格中显示多个属性页。  
  
3.  单击这些页并设置要应用到此点的显示属性。  
  
## <a name="see-also"></a>另请参阅  
 [地图（报表生成器和 SSRS）](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [按规则和分析数据更改多边形、线条和点的显示方式（报表生成器和 SSRS）](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)  
  
  
