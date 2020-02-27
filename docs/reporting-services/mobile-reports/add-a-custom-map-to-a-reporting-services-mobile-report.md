---
title: 向 Reporting Services 移动报表添加自定义地图 | Microsoft Docs
ms.date: 01/31/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: fd259b95-bb58-4eb1-a436-6aa12fc6f5f2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9410aac6b74fbb515010517a2fe0667f3c197802
ms.sourcegitcommit: 1b0906979db5a276b222f86ea6fdbe638e6c9719
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2020
ms.locfileid: "76971399"
---
# <a name="add-a-custom-map-to-a-reporting-services-mobile-report"></a>向 Reporting Services 移动报表添加自定义地图
自定义地图需要两个文件：  
* 针对几何形状的 .SHP 文件  
* 针对元数据的 .DBF 文件  
  
阅读有关 [Reporting Services 移动报表中的自定义地图](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md)的详细信息。  
  
将两个文件存储在同一文件夹中。 两个文件的文件名必须匹配（例如 canada.shp 和 canada.dbf）。 元数据（DBF 文件）的第一列用于与对应的形状名称（键）的键值匹配，并在使用数据填充地图时使用。
  
## <a name="load-a-custom-map"></a>加载自定义地图  
  
1. 在“布局”  选项卡上，选择地图类型：“渐变热度地图”  、“距离停止热度地图”  或“气泡图”  。将它拖到设计图面，并设置所需的大小。  
  
   ![SSMRP_MapsGallery](../../reporting-services/mobile-reports/media/ssmrp-mapsgallery.png)  
  
2. 在“布局”  视图 >“可视属性”  面板 >“地图”  中，选择“自定义地图来自文件”  。   
  
   ![SSMRP_SelectCustomMap](../../reporting-services/mobile-reports/media/ssmrp-selectcustommap.png)  
  
3. 在“打开”  对话框中，浏览到 SHP 和 DBF 文件的位置，然后选择这两个文件。   
  
   ![SSMRP_SelectDBFandSHP](../../reporting-services/mobile-reports/media/ssmrp-selectdbfandshp.png)  
  
## <a name="connect-data-to-a-custom-map"></a>将数据连接到自定义地图  
当第一次将自定义地图添加到报表时， [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] 使用模拟地理数据填充该地图。  
  
![SSMRP_MapsData](../../reporting-services/mobile-reports/media/ssmrp-mapsdata.png)  
  
在自定义地图中显示真实数据与在内置地图中显示数据相同。 请按照 [Reporting Services 移动报表中的地图](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md) 中的步骤来显示数据。  
  
### <a name="see-also"></a>另请参阅  
- [Custom maps in Reporting Services mobile reports](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md)  
- [Reporting Services 移动报表中的地图](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)  
- [使用 SQL Server Mobile Report Publisher 创建和发布移动报表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)   
  
  
  
  
