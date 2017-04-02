---
title: "Custom maps in Reporting Services mobile reports | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 59a4ebad-587a-4770-afcd-c69216b8afd9
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Custom maps in Reporting Services mobile reports
[!INCLUDE[PRODUCT_NAME](../../includes/product-name.md)] 中的地图使用称为 *ESRI 形状文件*的格式进行定义。  
  
该格式最初由一家私营公司设计，现在这种半开放格式被广泛应用于大部分 GIS 应用程序。 根据此格式， [!INCLUDE[PRODUCT_NAME](../../includes/short-product-name.md)] 需要提供两个文件来定义地图：  
  
- 针对几何形状的 .SHP 文件  
- 针对元数据的 .DBF 文件  
  
基本文件名称必须匹配（例如 *canada.shp* 和 *canada.dbf*）。 元数据必须包含对地图填充数据时要使用的字段 *NAME* ，该字段的值为对应的形状名称（键）的值。  
  
> **注意**：这两个地图文件 SHP 和 DBF 的大小加起来不能超过 512 KB。 如果地图文件太大，可以使用工具，例如 [http://mapshaper.org/](http://mapshaper.org/)，来减小其大小。  
  
请参阅如何 [将自定义地图添加到移动报表](../../reporting-services/mobile-reports/add-a-custom-map-to-a-reporting-services-mobile-report.md)。  
  
## 技术信息  
  
- 官方规范： [http://www.esri.com/library/whitepapers/pdfs/shapefile.pdf](http://www.esri.com/library/whitepapers/pdfs/shapefile.pdf)  
- 维基百科形状文件文章：[http://en.wikipedia.org/wiki/Shapefile](http://en.wikipedia.org/wiki/Shapefile)  
  
## 创建和编辑地图几何图形  
  
创建和编辑形状文件是一个复杂的过程，不属于本文档的讨论范围。 以下是一些可帮助你入门的资源和应用：  
  
- ArcGIS： [http://www.arcgis.com/](http://www.arcgis.com/)  
- 适用于 Adobe Illustrator 的 MAPublisher 插件： [http://www.avenza.com/mapublisher](http://www.avenza.com/mapublisher)  
- QuantumGIS（免费）： [http://www.qgis.org/](http://www.qgis.org/)  
- Manco 形状文件编辑器： [http://www.mancosoftware.com/ShapeFileEditor](http://www.mancosoftware.com/ShapeFileEditor)  
  
## 现有的形状文件  
  
许多现有的形状文件可从 Web 站点下载，例如：  
  
- Diva-GIS： [http://www.diva-gis.org/Data](http://www.diva-gis.org/Data)  
- OpenStreetMap： [http://openstreetmapdata.com/data](http://openstreetmapdata.com/data)  
- GeoCommons： [http://www.geocommons.com/](http://www.geocommons.com/)  
  
### 另请参阅  
- [Maps in Reporting Services mobile reports](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)  
- [使用 SQL Server 移动报表发布服务创建和发布移动报表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)   
  
  
  
