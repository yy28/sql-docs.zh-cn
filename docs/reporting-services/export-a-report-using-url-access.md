---
title: "将报表使用 URL 访问导出 |Microsoft 文档"
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
- formats [Reporting Services], URL rendering
- URL access [Reporting Services], rendering formats
ms.assetid: 6a3b7fc3-3d91-4d12-8371-42ea12e74517
caps.latest.revision: 42
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d9ee4dd3c00d9e250fd3c773a917ad3cf90f84c4
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="export-a-report-using-url-access"></a>使用 URL 访问导出报表
  可以选择使用 *rs:Format* URL 参数指定呈现报表的格式。  HTML4.0 和 HTM5 格式（呈现扩展插件）将呈现在浏览器中，对于其他格式，浏览器将会提示将报告输出保存到本地文件。  
  
 例如，若要直接从本机模式报表服务器获取报表的 PDF 副本：  
  
```  
http://myrshost/ReportServer?/myreport&rs:Format=PDF  
```  
  
 此外，若要从 SharePoint 集成模式的报表服务器获取：  
  
```  
http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/myrereport.rdl&rs:Format=PDF  
```  
  
 例如，浏览器中的以下 URL 命令从报表服务器的命名实例导出 PPTX 报表：  
  
```  
http://servername/ReportServer_THESQLINSTANCE/Pages/ReportViewer.aspx?%2freportfolder%2freport+name+with+spaces&rs:Format=pptx  
```  
  
 对于此参数，有效值为何随要访问的报表服务器上所安装的报表呈现扩展插件而异。 常见的扩展插件有 HTML4.0、MHTML、IMAGE、EXCELOPENXML (xlsx)、WORDOPENXML (docx)、CSV、PDF、XML 和 NULL。 如果指定的呈现扩展插件未安装在相应的报表服务器上，则相应报表将不能呈现，并将生成错误，同时通过浏览器来显示该错误。  
  
 如果未在 URL 中纳入 *Format* 参数，则报表服务器将检测浏览器，并将相应报表呈现为合适的 HTML 格式。  
  
## <a name="see-also"></a>另请参阅  
 [URL 访问 &#40;SSRS &#41;](../reporting-services/url-access-ssrs.md)   
 [URL 访问参数引用](../reporting-services/url-access-parameter-reference.md)  
  
  
