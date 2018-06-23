---
title: 地图视区属性对话框，优化 |Microsoft 文档
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
- sql12.rtp.rptdesigner.mapviewport.optimization.f1
- "10522"
ms.assetid: 8c0310ba-eedd-4c9f-95bd-1f9e2a1a8ed3
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 54606ed4dda94c569e1a4aef2438e42cd104eebd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130054"
---
# <a name="map-viewport-properties-dialog-box-optimization"></a>“地图视区属性”对话框 -&gt;“优化”
  针对 **“地图视区属性”** 对话框选择 **“优化”** 有助于控制用于在报表中查看地图的分辨率。  
  
 当在报表中嵌入空间数据时，分辨率越高，则意味着要在报表中存储的数据越多。 当不在报表中嵌入空间数据时，分辨率越高，则意味着报表处理器要花越多的时间创建地图细节。 分辨率越低，意味着等待报表呈现的时间量越少。  
  
 单击 **“表达式”** (*fx*) 按钮以编辑设置该选项的值的表达式。  
  
## <a name="options"></a>“常规”  
 **“性能”**  
 滑动指针使之靠近 **“性能”** 可简化地图并减少其显示细节。  
  
 **质量**  
 滑动指针使之靠近 **“质量”** 将以较高的明细程度绘制地图。  
  
 **地图分辨率**  
 指定地图分辨率。 此值指定您要在呈现的地图中看到的最小明细程度（点数）。  
  
## <a name="see-also"></a>请参阅  
 [地图（报表生成器和 SSRS）](report-design/maps-report-builder-and-ssrs.md)   
 [报表故障排除： 将报表映射&#40;报表生成器和 SSRS&#41;](report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md)  
  
  