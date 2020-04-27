---
title: SQL Server 2014 报表生成器的新增功能&#39;Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 8223c19b-4b0d-4b1d-a042-9a726c18e708
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 35ac6191407e02a2dc15ab210c5e9276e761df75
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66098675"
---
# <a name="what39s-new-in-report-builder-for-sql-server-2014"></a>SQL Server 2014 报表生成器的新增功能&#39;
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 引入了许多 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 功能。  
  
 有关此版本中有关其他[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]产品和技术的功能的信息，请参阅[SQL Server 2014 中的新增](../sql-server/what-s-new-in-sql-server-2016.md)功能。  
  
> [!TIP]  
>  有关此版本中新功能的最新信息和资源，请参阅有关[SQL Server Reporting Services （SSRS）中的新增功能的其他信息](https://go.microsoft.com/fwlink/?LinkId=207147)。  
  
##  <a name="excel-renderer-for-microsoft-excel-2007-2010-and-microsoft-excel-2003"></a><a name="ExcelRenderer"></a>用于 Microsoft Excel 2007-2010 和 Microsoft Excel 2003 的 Excel 呈现器  
 如果安装了针对 Word、Excel 和 PowerPoint 的 Microsoft Office 兼容包，[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中新增的 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Excel 呈现扩展插件可将报表呈现为能够兼容 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 2007-2010 及 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 2003 的 Excel 文档。 该格式为 Office Open XML，文件扩展名为 .xlsx。  
  
 此 Excel 呈现扩展插件消除了与 Excel 2003 兼容的早期版本的限制。 下面列出了呈现扩展插件中的改进：  
  
-   每个工作表的最大行数是 1,048,576。  
  
-   每个工作表的最大列数是 16,384。  
  
-   工作表中允许的颜色数目大约是 1600 万（24 位颜色）。  
  
-   ZIP 压缩提供较小的文件大小。  
  
 有关详细信息，请参阅 [导出到 Microsoft Excel（报表生成器和 SSRS）](report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md)中处理数据。  
  
##  <a name="word-renderer-for-microsoft-word-2007-2010-and-microsoft-word-2003"></a><a name="WordRenderer"></a>Microsoft Word 2007-2010 和 Microsoft Word 2003 的 word 呈现器  
 如果安装了针对 Word、Excel 和 PowerPoint 的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Office 兼容包，[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中新增的 [!INCLUDE[ofprword](../includes/ofprword-md.md)] Word 呈现扩展插件可将报表呈现为能够兼容 [!INCLUDE[ofprword](../includes/ofprword-md.md)] 2007-2010 及 [!INCLUDE[msCoName](../includes/msconame-md.md)] 2003 的 Word 文档。 该格式为 Office Open XML，文件扩展名为 docx。  
  
 除了使 Word 2007-2010 中的新增功能可用于导出的报表之外，导出的报表的 *.docx 文件往往更小。 通过使用 Word 呈现器导出的报表通常显著小于通过使用 Word 2003 呈现器导出的相同报表。  
  
 有关详细信息，请参阅 [导出到 Microsoft Word（报表生成器和 SSRS）](report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md)中处理数据。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 2014 中的报表生成器](report-builder/report-builder-in-sql-server-2016.md)  
  
  
