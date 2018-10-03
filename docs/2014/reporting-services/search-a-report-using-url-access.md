---
title: 使用 URL 访问搜索报表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- searching reports
- text searches [Reporting Services]
- URL access [Reporting Services], report searches
ms.assetid: 6f3410c4-7944-448f-bae8-bab3e8152d46
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9ffac7320bc284547a8b5d0598c5523e5c0b09b8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48141697"
---
# <a name="search-a-report-using-url-access"></a>使用 URL 访问搜索报表
  可以使用 URL 访问在报表中搜索一组特定的文本。 若要在报表中搜索，请将 URL 中的 *rc:FindString* 参数的值设置为等于所要搜索的文本。 另外，可以使用 *rc:StartFind* 和 *rc:EndFind* 参数将搜索范围缩小到相应报表中的特定页。  
  
## <a name="example"></a>示例  
 下面的 URL 访问示例在 Product Catalog 示例报表的第 1 页到第 5 页之间搜索第一条“Mountain-400”文本：  
  
```  
http://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
```  
  
## <a name="see-also"></a>请参阅  
 [URL 访问&#40;SSRS&#41;](url-access-ssrs.md)   
 [URL 访问参数引用](url-access-parameter-reference.md)  
  
  
