---
title: "\"地图视区属性\" 对话框-\"常规\" |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.mapviewport.general.f1
- "10505"
ms.assetid: 6c9c773e-5c56-4571-95ed-8a157cfdfe52
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8ec0aaa051ba317cd05a9784c80fb997f5fa19e6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108237"
---
# <a name="map-viewport-properties-dialog-box-general"></a>“地图视区属性”对话框 -&gt;“常规”
  选择 **“地图视区属性”** 对话框中的 **“常规”** 可以更改坐标系统、投影和边界选项。  
  
## <a name="options"></a>选项  
 **坐标系统**  
 指示地图数据使用的坐标系统的类型。  
  
-   **平面**当地图数据处于 X 和 Y 坐标（例如，用于生成计划）时，请选择此选项。  
  
-   **地理位置**当地图数据处于经度和纬度坐标中时（例如，对于城市位置），请选择此选项。  
  
 **投影**  
 指定用于将地理坐标投影到二维图面的方法。 选择与将要可视化的数据兼容的投影。 受投影影响的四个空间属性是区域、形状、距离和方向。 对于地球的视图，投影的选择取决于中心视图、地图边界和缩放系数。  
  
 以下的每个投影具有这些空间属性的一个或多个：  
  
-   **Equirectangular**选择此选项可将经度和纬度用作矩形坐标。  
  
-   **Mercator**对于较小的区域，请选择此常用投影，使赤道的扭曲较少，或者当你想要添加具有使用 Mercator 投影的现有图块层的地图层时。  
  
-   **Robinson**选择此选项可减少从赤道到两极的大型区域的扭曲。 由 Arthur H. Robinson 在 1963 年开发。  
  
-   **Fahey**选择此选项可减少从赤道到两极的大型区域的扭曲。 由 Lawrence Fahey 在 1975 年开发。  
  
-   **Eckert1**如果选择此选项，则在纬度中使用均匀间距的等效项，在经线中使用直线。  
  
-   **Eckert3**如果选择此选项，则在纬度和经线的曲线中使用均匀间距的等效项。  
  
-   **HammerAitoff**对于极坐标图或世界地图，请选择此选项。  
  
-   **Wagner3**对于世界地图，请选择此选项。  
  
-   **Bonne**选择此选项可在一只是在阿特拉斯中看到世界。  
  
 **分页符选项**  
 选择所需选项以指示如何调整内容以使其适合报表页面。  
  
 **边界选项**  
 指定坐标的上边界和下边界，以控制在报表中出现的地图部分。  
  
 **最小 X**  
 最小 X 值。 仅适用于 **“平面数据”** 。  
  
 **最大 X**  
 最大 X 值。 仅适用于 **“平面数据”** 。  
  
 **最小 Y**  
 最小 Y 值。 仅适用于 **“平面数据”** 。  
  
 **最大 Y**  
 最大 Y 值。 仅适用于 **“平面数据”** 。  
  
 **最低经度**  
 最低经度值。 仅适用于 **“地理”** 。  
  
 **最高经度**  
 最高经度值。 仅适用于 **“地理”** 。  
  
 **最低纬度**  
 最低纬度值。 仅适用于 **“地理”** 。  
  
 **最高纬度**  
 最高纬度值。 仅适用于 **“地理”** 。  
  
## <a name="see-also"></a>另请参阅  
 [地图（报表生成器和 SSRS）](report-design/maps-report-builder-and-ssrs.md)  
  
  
