---
title: Reporting Services 移动报表中的自定义地图 | Microsoft Docs
description: 了解 SQL Server 移动报表发布服务器中使用称为 ESRI 形状文件的格式进行定义的地图。
ms.date: 12/06/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: 59a4ebad-587a-4770-afcd-c69216b8afd9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 17975defea6029e4077acbe45fd3f8b0d7495267
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53212076"
---
# <a name="custom-maps-in-reporting-services-mobile-reports"></a>Custom maps in Reporting Services mobile reports
SQL Server 移动报表发布服务器中的地图使用称为 ESRI 形状文件的格式进行定义。  
  
该格式最初由一家私营公司设计，现在这种半开放格式被广泛应用于大部分 GIS 应用程序。 根据此格式，移动报表发布服务器需要提供两个文件来定义地图：  
  
- 针对几何形状的 .SHP 文件  
- 针对元数据的 .DBF 文件  
  
基本文件名称必须匹配（例如 *canada.shp* 和 *canada.dbf*）。 元数据必须包含对地图填充数据时要使用的字段 *NAME* ，该字段的值为对应的形状名称（键）的值。  

这两个地图文件 SHP 和 DBF 的大小加起来不能超过 512 KB。 如果地图文件太大，可以使用工具，例如 [https://mapshaper.org/](https://mapshaper.org/)，来减小其大小。  
  
请参阅如何 [将自定义地图添加到移动报表](../../reporting-services/mobile-reports/add-a-custom-map-to-a-reporting-services-mobile-report.md)。  
  
## <a name="technical-information"></a>技术信息  
  
- 官方规范：[https://www.esri.com/library/whitepapers/pdfs/shapefile.pdf](https://www.esri.com/library/whitepapers/pdfs/shapefile.pdf)  
- Wikipedia 形状文件文章：[https://en.wikipedia.org/wiki/Shapefile](https://en.wikipedia.org/wiki/Shapefile)  
  
## <a name="creating--editing-map-geometry"></a>创建和编辑地图几何图形  
  
创建和编辑形状文件是一个复杂的过程，不属于本文档的讨论范围。 以下是一些可帮助你入门的资源和应用：  
  
- ArcGIS：[https://www.arcgis.com/](https://www.arcgis.com/)  
- Adobe Illustrator 的 MAPublisher 插件：[https://www.avenza.com/mapublisher](https://www.avenza.com/mapublisher)  
- QuantumGIS（免费）：[https://www.qgis.org/](https://www.qgis.org/)  

## <a name="existing-shapefiles"></a>现有的形状文件  
  
许多现有的形状文件都可从 Web 站点下载，例如 Diva-GIS：[https://www.diva-gis.org/Data](https://www.diva-gis.org/Data)。  

## <a name="see-also"></a>另请参阅  
- [Maps in Reporting Services mobile reports](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)  
- [使用 SQL Server 移动报表发布服务创建和发布移动报表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)   
  
  
  
