---
title: "导入和导出知识 | Microsoft Docs"
ms.custom: 
ms.date: 07/31/2012
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 12537c9d-31e4-40b0-a411-cb343abbe96a
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a0963e7fc98cc0489d6f93c2381b701bd26ef569
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="importing-and-exporting-knowledge"></a>导入和导出知识
  您可以在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 应用程序中直接创建知识库和域，也可以将知识导入到知识库中或从知识库中导出知识。 在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 应用程序中，您可以使用某一数据文件执行导入和导出操作，也可以使用 Excel 文件执行导入操作。 使用的数据文件是由 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 创建的扩展名为 .dqs 的加密文件。 由 Microsoft Excel 创建的文件可以具有 .xlsx、.xls 或 .csv 扩展名。 这些操作使您可以更灵活地生成和共享用于执行数据清理和匹配的知识。  
  
> [!IMPORTANT]  
>  您可以通过从命令提示符处运行 DQSInstaller.exe 文件，一次将 *中的*[!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] “所有”知识库导出到某一 DQS 备份文件 (.dqsb)。 同样，您可以通过从命令提示符处运行 DQSInstaller.exe 文件，一次将某一 DQS 备份文件 (.dqsb) 中的  “所有”知识库导入到 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 中。 有关此操作的信息，请参阅 DQS 安装指南中的 [Export and Import DQS Knowledge Bases Using DQSInstaller.exe](../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md) 。  
  
## <a name="in-this-section"></a>本节内容  
 您可以执行下列导入和导出操作：  
  
|||  
|-|-|  
|将知识库中的域导出到 .dqs 数据文件中|[将域导出到 .dqs 文件](../data-quality-services/export-a-domain-to-a-dqs-file.md)|  
|将域从 .dqs 数据文件导入到现有知识库中|[从 .dqs 文件导入域](../data-quality-services/import-a-domain-from-a-dqs-file.md)|  
|将整个知识库导出到 .dqs 数据文件中|[将知识库导出到 .dqs 文件](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)|  
|将整个知识库导入到 .dqs 数据文件中|[从 .dqs 文件导入知识库](../data-quality-services/import-a-knowledge-base-from-a-dqs-file.md)|  
|将值从 Excel 文件导入到域|[Import Values from an Excel File into a Domain](../data-quality-services/import-values-from-an-excel-file-into-a-domain.md)|  
|将域从 Excel 文件中导入到知识库中|[从知识发现中的 Excel 文件导入域](../data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md)|  
|将在清理过程中收集的知识导入到知识库中|[将清理项目值导入域](../data-quality-services/import-cleansing-project-values-into-a-domain.md)|  
  
## <a name="related-tasks"></a>相关任务  
  
|任务说明|主题|  
|----------------------|-----------|  
|通过运行知识发现并以交互方式管理知识来生成知识库|[生成知识库](../data-quality-services/building-a-knowledge-base.md)|  
|创建单一域，并将知识添加到该域中。|[管理域](../data-quality-services/managing-a-domain.md)|  
|创建一个复合域，并将知识添加到该域中。|[管理复合域](../data-quality-services/managing-a-composite-domain.md)|  
  
  
