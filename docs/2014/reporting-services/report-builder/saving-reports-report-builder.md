---
title: 保存报表（报表生成器）| Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 59ddc4b8-9517-4d3f-9c88-a07e9907cecb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e21b1c9e48dcccf8b72a60fbd381aac3d878c0dc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66107633"
---
# <a name="saving-reports-report-builder"></a>保存报表（报表生成器）
  在报表生成器中，可以将报表保存到您有写入权限的报表服务器、SharePoint 库和文件共享区，也可以将其保存到您的计算机。 可以将报表保存到打开报表时的相同位置或将其保存到其他位置，也可以使用新名称将报表保存到相同或不同位置。 默认情况下，将报表重新保存到与其打开位置相同的位置。 保存报表时，真正保存的内容是报表定义，该定义描述了报表布局。 您不是在保存数据。 每次运行报表时，报表数据将刷新，它可能不同于您上次运行报表时的数据。  
  
 如果要将报表保存为另一格式或同时保存报表定义和数据，请使用以下 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能之一：  
  
-   将呈现的报表导出为另一文件格式，如逗号分隔文件 (CSV) 或 Excel 工作簿，然后以该格式保存报表。 还可以从报表生成数据馈送并保存报表数据。  
  
-   创建报表订阅以便传递和将报表保存到文件共享区。  
  
-   使用报表历史记录功能将所呈现报表的各个版本作为历史记录副本保存。  
  
 若要了解有关直接在报表服务器上查看和管理报表的详细信息，请参阅 msdn.microsoft.com 上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [联机丛书](https://go.microsoft.com/fwlink/?LinkId=154888)中的[查找、查看和管理报表（报表生成器和 SSRS）](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)和 [Reporting Services 报表服务器（本机模式）](../report-server/reporting-services-report-server-native-mode.md)。  
  
##  <a name="saving-report-definitions"></a><a name="SavingReportDefinitions"></a>保存报表定义  
 尽管可以将报表保存到您的计算机，但是将报表保存到报表服务器更有利。  
  
 将报表保存到报表服务器具有以下优势：  
  
-   报表可供其他有权访问您保存报表的文件夹的用户使用。  
  
-   可以使用报表管理器来管理和查看报表。  
  
-   将报表资源（如数据源、图像和子报表）存储在一个位置以便于访问。  
  
-   可以通过订阅将报表传递给其他用户。  
  
-   报表安全存储在报表服务器数据库中。  
  
-   可以记录报表运行情况，提供性能和审核信息。  
  
 将报表保存到报表服务器也称为发布报表。 保存报表时，只是保存报表定义。 每次运行报表时，报表数据将刷新，它可能不同于您上次运行报表时的数据。 如果要同时保存报表定义和数据，应使用报表历史记录功能。 使用此功能，您可以保存包含报表数据的报表副本。  
  

  
##  <a name="exporting-and-saving-reports"></a><a name="ExportingAndSavingReports"></a> 导出和保存报表  
 如果只有少量要存档的报表，可以考虑导出报表并将其另存为文件。 在将报表导出到其他应用程序（如 PDF 或 Excel）后，您可以将其另存为文件，并放在网络上受保护的共享目录中。 或者，如果希望在报表服务器数据库中保留报表的所有副本（不论何种格式），则可以将已保存的 PDF 或 Excel 文件作为资源项上载。 有关导出报表的详细信息，请参阅将[报表导出 &#40;报表生成器和 SSRS&#41;](export-reports-report-builder-and-ssrs.md)并[将文件或报表 &#40;报表管理器&#41;上传](../reports/upload-a-file-or-report-report-manager.md)。  
  

  
##  <a name="using-file-share-delivery"></a><a name="UsingFileShareDelivery"></a> 使用文件共享传递  
 如果有大量要存档的报表，则可以创建订阅，将报表直接传递到文件系统。 对于这种方法，您必须为每个报表创建订阅，选择存储这些报表的共享文件夹，并制订用于指定文件创建时间的计划。 一旦定义订阅，报表服务器即可在无人参与的情况下运行报表，并且使用提供的计划存档报表文件。 如果只是偶尔存档报表，您也可以创建一次性的计划。 有关订阅和文件共享传递的详细信息，请参阅 SQL Server 联机丛书中 [Reporting Services 文档](https://go.microsoft.com/fwlink/?linkid=121312) 中的“Reporting Services 中的文件传递”。  
  

  
##  <a name="using-report-history"></a><a name="UsingReportHistory"></a> 使用报表历史记录  
 您还可以使用报表历史记录功能创建历史记录副本。 随后，您可以备份报表服务器数据库，将备份内容存储在安全的位置，以备将来使用。 所有报表历史记录（连同报表、共享数据源项、文件夹、订阅和共享计划）都存储在报表服务器数据库中。 您可以通过创建备份来维护报表历史记录和元数据（如指定报表接收人的订阅信息）的永久副本。 有关详细信息，请参阅 SQL Server 联机丛书中 [Reporting Services 文档](https://go.microsoft.com/fwlink/?linkid=121312) 中的“管理报表历史记录”。  
  

  
##  <a name="how-to-topics"></a><a name="HowTo"></a>操作指南主题  
  
-   [将报表保存到报表服务器（报表生成器）](save-reports-to-a-report-server-report-builder.md)  
  
-   [将报表保存到 SharePoint 库（报表生成器）](save-a-report-to-a-sharepoint-library-report-builder.md)  
  
-   [将报表保存到计算机 &#40;报表生成器&#41;](../save-reports-to-your-computer-report-builder.md)  
  

  
## <a name="see-also"></a>另请参阅  
 [报表、报表部件和报表定义 &#40;报表生成器和 SSRS&#41;](../report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [安装、卸载和报表生成器支持](../install-uninstall-and-report-builder-support.md)   
 [查找、查看和管理 &#40;报表生成器和 SSRS 的报表 &#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [导出报表 &#40;报表生成器和 SSRS&#41;](export-reports-report-builder-and-ssrs.md)   
 [打印报表（报表生成器和 SSRS）](print-reports-report-builder-and-ssrs.md)  
  
  
