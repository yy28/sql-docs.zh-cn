---
title: 向地图添加自定义位置（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- MICROSOFT.REPORTDESIGNER.MAPPOINT.POINTTEMPLATE
ms.assetid: 7d36faae-5bcc-446a-9eba-f42349cafacb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e5961a4d4984a4da5abd788903a05789de862db7
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59950863"
---
# <a name="add-custom-locations-to-a-map-report-builder-and-ssrs"></a>向地图添加自定义位置（报表生成器和 SSRS）
  向报表添加地图之后，可以添加您自己的点位置。  
  
 通过设置层的点属性的选项来控制层上所有点的显示属性。 对于所选的嵌入点，可以覆盖这些显示属性。  
  
> [!NOTE]  
>  覆盖该嵌入点的层显示属性时，您所做的更改无法还原。  
  
 有关详细信息，请参阅 [按规则和分析数据更改多边形、线条和点的显示方式（报表生成器和 SSRS）](vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-point-layer"></a>添加点层  
  
1.  在报表设计图面中，单击该地图以选择它并显示“地图”窗格。  
  
2.  在工具栏中，单击 **“添加层”**。  
  
3.  从下拉列表中，单击“添加点层”。 将不包含点的点层添加到该地图。 默认情况下，为嵌入的点准备了点层。  
  
### <a name="to-add-a-custom-point"></a>添加自定义点  
  
1.  在报表设计图面中，单击该地图以选择它并显示“地图”窗格。  
  
2.  在“地图”窗格中，右键单击具有类型“嵌入”的点层，然后单击“添加点”。 光标将变为十字准线。  
  
3.  若要添加点，请单击地图上的某个位置。 在您单击的位置将嵌入的点添加到所选层中。  
  
### <a name="to-customize-the-display-for-an-embedded-point"></a>自定义嵌入点的显示方式  
  
1.  右键单击该点，然后单击“点属性”。 将打开 **“地图嵌入点属性”** 对话框。  
  
2.  单击 **“覆盖此层的点选项”**。 将在左窗格中显示多个属性页。  
  
3.  单击这些页并设置要应用到此点的显示属性。  
  
## <a name="see-also"></a>请参阅  
 [地图（报表生成器和 SSRS）](maps-report-builder-and-ssrs.md)   
 [按规则和分析数据更改多边形、线条和点的显示方式（报表生成器和 SSRS）](vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)  
  
  
