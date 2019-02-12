---
title: 地图视区属性对话框，常规 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.mapviewport.general.f1
- "10505"
ms.assetid: 6c9c773e-5c56-4571-95ed-8a157cfdfe52
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: 33849743e47ad910fad44938e7537d7b4be8624a
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56018179"
---
# <a name="map-viewport-properties-dialog-box-general"></a>“地图视区属性”对话框 -&gt;“常规”
  选择 **“地图视区属性”** 对话框中的 **“常规”** 可以更改坐标系统、投影和边界选项。  
  
## <a name="options"></a>选项  
 **坐标系统**  
 指示地图数据使用的坐标系统的类型。  
  
-   **平面数据** 当地图数据用 X 和 Y 坐标表示时选择此选项，例如用于建筑物规划。  
  
-   **地理** 当地图数据用经度和纬度坐标表示时选择此选项，例如用于城市位置。  
  
 **Projection**  
 指定用于将地理坐标投影到二维图面的方法。 选择与将要可视化的数据兼容的投影。 受投影影响的四个空间属性是区域、形状、距离和方向。 对于地球的视图，投影的选择取决于中心视图、地图边界和缩放系数。  
  
 以下的每个投影具有这些空间属性的一个或多个：  
  
-   **Equirectangular** 选择此选项以将经度和纬度作为矩形坐标。  
  
-   **Mercator** 选择此常用投影用于赤道周围扭曲较少的较小区域，或者当您要添加具有使用 Mercator 投影的现有图块层的地图层时选择它。  
  
-   **Robinson** 选择此选项用于从赤道到极地的扭曲较少的大区域。 由 Arthur H. Robinson 在 1963 年开发。  
  
-   **Fahey** 选择此选项用于从赤道到极地的扭曲较少的大区域。 由 Lawrence Fahey 在 1975 年开发。  
  
-   **Eckert1** 选择此选项可以使用等距的纬线和为直线的经线。  
  
-   **Eckert3** 选择此选项可以使用等距的纬线和为曲线的经线。  
  
-   **HammerAitoff** 选择此选项用于极地地图或世界地图。  
  
-   **Wagner3** 选择此选项用于世界地图。  
  
-   **Bonne** 选择此选项可以查看地图中的各地地貌和城市等。  
  
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
  
 **最小经度**  
 最低经度值。 仅适用于 **“地理”** 。  
  
 **最大经度**  
 最高经度值。 仅适用于 **“地理”** 。  
  
 **最低纬度**  
 最低纬度值。 仅适用于 **“地理”** 。  
  
 **最高纬度**  
 最高纬度值。 仅适用于 **“地理”** 。  
  
## <a name="see-also"></a>请参阅  
 [地图（报表生成器和 SSRS）](report-design/maps-report-builder-and-ssrs.md)  
  
  
