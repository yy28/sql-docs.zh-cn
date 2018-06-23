---
title: 地图视区属性对话框中，中心和缩放 |Microsoft 文档
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
- sql12.rtp.rptdesigner.mapviewport.centerandzoom.f1
- "10506"
ms.assetid: 642a06f5-293f-48e0-97a6-1489dbefa719
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: c3c75a22ee1a367f752cd310a19aebdb241c90eb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025657"
---
# <a name="map-viewport-properties-dialog-box-center-and-zoom"></a>“地图视区属性”对话框 -&gt;“中心和缩放”
  选择 **“地图视区属性”** 对话框中的 **“中心和缩放”** 可以设置地图的中心视图和缩放系数。 指定地图数据源和要在报表中包含的地图的边界后，可以指定视图中心和缩放系数以进一步控制地图的显示。 根据用于指定中心和缩放值的不同方法，选项也会不同。 单击 **“表达式”** (*fx*) 按钮以编辑设置该选项的值的表达式。  
  
## <a name="options"></a>“常规”  
 **设置视图中心和缩放级别**  
 选择此选项可以指定视图中心和缩放级别的自定义值。  
  
 **将地图居中以显示地图层**  
 选择此选项可以指定一个层并自动使视图位于其地图数据的中心。 例如，使视图位于 LineLayer1 的中心。  
  
 **将地图居中以显示嵌入的地图元素**  
 选择此选项可以使视图位于特定的数据绑定地图元素的中心。 空间数据必须与分析数据具有某种关系才能指定此选项。  
  
 例如，将视图位于这样的地图元素中心：匹配字段的名称为 [City] 且匹配值为“Seattle”。  
  
 **将地图居中以显示所有数据绑定地图元素**  
 选择此选项可以将视图位于此层中所有地图元素的中心。 空间数据必须与分析数据具有某种关系才能指定此选项。  
  
 例如，将视图位于显示城市的多边形气泡图层的中心，且气泡大小与人口数有关。 在计算视区的中心时，只包括具有匹配人口数值的那些城市。  
  
 **中心和缩放选项**  
 选择一个选项来指定视图中心和缩放级别。  
  
 **视图中心 (X) %**  
 水平坐标。 默认值 50% 表示 将视图中心位于最小水平值和最大水平值之间的中点。  
  
 **视图中心 (Y) %**  
 垂直坐标。 默认值 50% 表示将视图中心位于最小垂直值和最大垂直值之间的中点。  
  
 **缩放级别 （%）**  
 缩放系数。 默认值 100% 表示不放大。  
  
 **在此层上的中心视图**  
 指定层的名称。  
  
 **与此条件匹配，使地图元素的中心视图**  
 显示的只读字段用于将地图数据与分析数据匹配。 指定要匹配的值。 视图将自动在此地图元素上居中。 例如，NAME = TEXAS。 默认情况下，条件的数据类型是 String 且匹配区分大小写。  
  
 若要匹配具有不同数据类型的字段，必须编写一个计算结果为该数据类型的表达式。 例如，如果匹配字段为存储为整数的 5 个数字的邮政编码，则若要指定邮政编码 98053，必须使用表达式 =98053。  
  
## <a name="see-also"></a>请参阅  
 [地图（报表生成器和 SSRS）](report-design/maps-report-builder-and-ssrs.md)  
  
  