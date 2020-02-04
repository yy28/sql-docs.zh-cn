---
title: 保存报表（报表生成器）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 59ddc4b8-9517-4d3f-9c88-a07e9907cecb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8682d55f6c805066f5b596e79a074f253db9faa9
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "66499631"
---
# <a name="saving-reports-report-builder"></a>保存报表（报表生成器）
  在报表生成器中，可以将分页报表保存到你有写入权限的 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 报表服务器、SharePoint 库和文件共享，也可以将其保存到你的计算机。 
  
保存报表时，真正保存的内容是报表定义，该定义描述了报表布局。 您不是在保存数据。 每次运行报表时，报表数据将刷新，它可能不同于您上次运行报表时的数据。  
  
 如果要将报表保存为另一格式或同时保存报表定义和数据，请使用以下 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能之一：  
  
-   将呈现的报表导出为另一文件格式，如逗号分隔文件 (CSV) 或 Excel 工作簿，然后以该格式保存报表。 还可以从报表生成数据馈送并保存报表数据。  
  
-   创建报表订阅以便传递和将报表保存到文件共享区。  
  
-   使用报表历史记录功能将所呈现报表的各个版本作为历史记录副本保存。  
  
 若要了解有关直接在报表服务器上查看和管理报表的详细信息，请参阅[查找、查看和管理报表（报表生成器和 SSRS）](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)和 [Reporting Services 报表服务器（本机模式）](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)。  
  
##  <a name="SavingReportDefinitions"></a> 将报表保存到报表服务器  
  将报表保存到报表服务器也称为发布报表。 尽管可以将报表保存到计算机，但是将报表保存到报表服务器更有利：  
  
-   报表可供其他有权访问您保存报表的文件夹的用户使用。  
  
-   可以使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web 门户来管理和查看报表。  
  
-   将报表资源（如数据源、图像和子报表）存储在一个位置以便于访问。  
  
-   可以通过订阅将报表传递给其他用户。  
  
-   报表安全存储在报表服务器数据库中。  
  
-   可以记录报表运行情况，提供性能和审核信息。  
  
##  <a name="ExportingAndSavingReports"></a> 导出和保存报表  
 如果只有少量要存档的报表，可以考虑导出报表并将其另存为文件。 在将报表导出到其他应用程序（如 PDF 或 Excel）后，您可以将其另存为文件，并放在网络上受保护的共享目录中。 或者，如果希望在报表服务器数据库中保留报表的所有副本（不论何种格式），则可以将已保存的 PDF 或 Excel 文件作为资源项上载。 有关导出报表的详细信息，请参阅 [导出报表（报表生成器和 SSRS）](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md) 和 [上传文件或报表](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)。  
  
##  <a name="UsingFileShareDelivery"></a> 使用文件共享传递  
 如果有大量要存档的报表，则可以创建订阅，将报表直接传递到文件系统。 对于这种方法，您必须为每个报表创建订阅，选择存储这些报表的共享文件夹，并制订用于指定文件创建时间的计划。 一旦定义订阅，报表服务器即可在无人参与的情况下运行报表，并且使用提供的计划存档报表文件。 如果只是偶尔存档报表，您也可以创建一次性的计划。 有关订阅和文件共享传递的详细信息，请参阅 [Reporting Services 中的文件共享传递](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)。  
  
##  <a name="UsingReportHistory"></a> 使用报表历史记录  
 您还可以使用报表历史记录功能创建历史记录副本。 随后，您可以备份报表服务器数据库，将备份内容存储在安全的位置，以备将来使用。 所有报表历史记录（连同报表、共享数据源项、文件夹、订阅和共享计划）都存储在报表服务器数据库中。 您可以通过创建备份来维护报表历史记录和元数据（如指定报表接收人的订阅信息）的永久副本。 有关详细信息，请参阅 [创建、修改和删除报表历史记录中的快照](../../reporting-services/report-server/create-modify-and-delete-snapshots-in-report-history.md)。  
 
##  <a name="HowTo"></a> 操作指南主题  
  
-   [将报表保存到报表服务器（报表生成器）](../../reporting-services/report-builder/save-reports-to-a-report-server-report-builder.md)  
  
-   [将报表保存到 SharePoint 库（报表生成器）](../../reporting-services/report-builder/save-a-report-to-a-sharepoint-library-report-builder.md)  
   
## <a name="see-also"></a>另请参阅  
 [报表、报表部件和报表定义（报表生成器和 SSRS）](../../reporting-services/report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [Install Report Builder](../install-windows/install-report-builder.md)   
 [查找、查看和管理报表（报表生成器和 SSRS）](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [导出报表（报表生成器和 SSRS）](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [打印报表（报表生成器和 SSRS）](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)  
  
  
