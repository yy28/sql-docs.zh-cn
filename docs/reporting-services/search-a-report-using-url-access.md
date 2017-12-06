---
title: "使用 URL 访问搜索报表 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- searching reports
- text searches [Reporting Services]
- URL access [Reporting Services], report searches
ms.assetid: 6f3410c4-7944-448f-bae8-bab3e8152d46
caps.latest.revision: "34"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6de1f0cb87292513b0765a5653ce1cabcacdf105
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="search-a-report-using-url-access"></a>使用 URL 访问搜索报表
  可以使用 URL 访问在报表中搜索一组特定的文本。 若要在报表中搜索，请将 URL 中的 *rc:FindString* 参数的值设置为等于所要搜索的文本。 另外，可以使用 *rc:StartFind* 和 *rc:EndFind* 参数将搜索范围缩小到相应报表中的特定页。  
  
## <a name="example"></a>示例  
 下面的 URL 访问示例在 Product Catalog 示例报表的第 1 页到第 5 页之间搜索第一条“Mountain-400”文本：  
  
```  
http://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
```  
  
## <a name="see-also"></a>另请参阅  
 [URL 访问 (SSRS)](../reporting-services/url-access-ssrs.md)   
 [URL 访问参数引用](../reporting-services/url-access-parameter-reference.md)  
  
  
