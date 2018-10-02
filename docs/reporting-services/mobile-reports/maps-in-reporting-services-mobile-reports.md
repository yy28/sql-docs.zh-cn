---
title: Reporting Services 移动报表中的地图 | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 50658295-a71c-441e-8eba-e1ef066629c0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5b09c8aec100d877256f0d8d9b4b97530ecdf5c6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47810986"
---
# <a name="maps-in-reporting-services-mobile-reports"></a>Maps in Reporting Services mobile reports
地图是实现地理数据可视化效果的好办法。 [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)] 提供三种不同类型的地图可视化，并且内置了各个洲和不同国家/地区的地图。 你也可以 [上载和使用自定义地图](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md)。   
  
## <a name="types-of-maps"></a>地图类型  
  
SQL Server 移动报表提供了三种不同类型的地图，分别适用于不同的情况。  
  
![SSMRP_MapsGallery](../../reporting-services/mobile-reports/media/ssmrp-mapsgallery.png)  
  
**渐变热度地图** 值属性中的字段显示为地图中每个区域所填充的一种颜色的深浅。 你可以在“值方向”框中设置更大的值还是更小的值的颜色较深。   
  
**气泡图** 值属性确定关联的区域上显示的气泡可视化对象的半径。 你可以设置所有气泡具有相同颜色还是各有不同颜色。   
  
**区域停止点热度地图** 显示相对于目标的值。 **目标** 属性确定“比较”字段和“值”字段之间的增量。 产生的增量确定了填充地图的相关联区域的颜色，从绿色到黄色再到红色。 你可以在“值方向”框中设置更大的值还是更小的值的颜色为绿色。   
  
## <a name="select-the-map-type-and-region"></a>选择地图类型和区域  
  
1. 在“布局”选项卡中选择一个地图类型，将其拖到设计图面，并将其大小调整为你所需的大小。  
  
2. 在“布局”视图>“视觉属性”面板>“地图”中，选择你所需的特定地图区域。  
  
   ![SSMRP_SelectMap](../../reporting-services/mobile-reports/media/ssmrp-selectmaps.png)  
  
3. 对于辐射热度地图和区域停止点热度地图，请在“视觉属性”下方的“值方向”框中设置更高值还是更低值较好。  
  
7. 对于气泡图，请在“视觉属性”下方将“使用不同颜色”设置为“开”或“关”，以便将气泡颜色设置为同一颜色或者是各不相同的颜色。  
  
## <a name="select-the-map-data"></a>选择地图数据  
当第一次将地图添加到报表时， [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] 使用模拟地理数据填充该地图。  
  
![SSMRP_MapsData](../../reporting-services/mobile-reports/media/ssmrp-mapsdata.png)  
  
若要在地图中显示真实数据，需要设置至少两个地图数据属性的值：   
* **键** 属性将数据连接到特定的地图区域，例如美国的州，或者是在非洲的地区。  
* **值** 属性是一个数值字段，与所选的键字段位于相同的表中。 这些值在不同地图中以不同方式表示。 **渐变图** 使用这些值来根据值的范围使用不同的颜色深浅度设置每个区域的颜色。 **气泡图** 基于值属性来确定每个区域上的气泡可视化对象的大小。   
* 对于区域停止点热度地图，还需要设置 **目标** 属性。  
  
### <a name="set-map-data-properties"></a>设置地图数据属性  
  
1. 在左上角选择“数据”  选项卡。  
  
2. 选择“添加数据”，然后选择“本地 Excel”或“SSRS 服务器”。  
  
   > **提示**：请确保 [数据的格式为可用于移动报表的格式](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md)。  
  
3. 选择需要的工作表，并选择“导入” 。  
   你可以在 [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)]中看到你的数据。  
  
4. 在“数据”视图 >“数据属性”面板 >“键”下面，在左侧的框中选择包含地图数据的表，然后在右侧的框中选择与你的地图中的区域相匹配的键字段。  
  
5. 在“值”的下方，相同的表已在左侧框中。 选择要在地图上显示其值的数值字段。   
  
6. 如果是区域停止点热度地图，则在“目标”  框的下方，相同的表位于左侧框中。 在右侧框中，选择要将其值作为目标值的数值字段。   
  
   ![SSMRP_MapRangeHeatData](../../reporting-services/mobile-reports/media/ssmrp-maprangeheatdata.png)  
  
7. 选择左上角的“预览”  。  
  
   ![SSMRP_MapRangeHeatPreview](../../reporting-services/mobile-reports/media/ssmrp-maprangeheatpreview.png)  
     
8. 在左上角选择“保存”图标，然后选择“保存在本地”或“保存到服务器”。  
  
### <a name="see-also"></a>另请参阅  
-  [Custom maps in Reporting Services mobile reports](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md)  
- [使用 SQL Server Mobile Report Publisher 创建和发布移动报表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
  
  
