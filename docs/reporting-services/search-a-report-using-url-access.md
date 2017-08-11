---
title: "使用 URL 访问报表中搜索 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 39ec7f9885cff6bcfcbf65e0448f3e8e837bc8a6
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="search-a-report-using-url-access"></a>使用 URL 访问搜索报表
  可以使用 URL 访问在报表中搜索一组特定的文本。 若要在报表中搜索，请将 URL 中的 *rc:FindString* 参数的值设置为等于所要搜索的文本。 另外，可以使用 *rc:StartFind* 和 *rc:EndFind* 参数将搜索范围缩小到相应报表中的特定页。  
  
## <a name="example"></a>示例  
 下面的 URL 访问示例在 Product Catalog 示例报表的第 1 页到第 5 页之间搜索第一条“Mountain-400”文本：  
  
```  
http://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
```  
  
## <a name="see-also"></a>另请参阅  
 [URL 访问 &#40;SSRS &#41;](../reporting-services/url-access-ssrs.md)   
 [URL 访问参数引用](../reporting-services/url-access-parameter-reference.md)  
  
  
