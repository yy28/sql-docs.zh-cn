---
title: 发布报表 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], publishing
- publishing reports [Reporting Services]
ms.assetid: ef5a514e-e818-4041-a8b0-15835f9a046b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 86ab056f18e69b0b264525377efb0d257ebc2b95
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108031"
---
# <a name="publish-reports"></a>发布报表
  从[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，你可以通过部署报表服务器项目将项目中的所有报表和共享数据源发布到报表服务器，也可以发布单个报表。 在可以发布报表之前，必须指定目标报表服务器的 URL。 有关详细信息，请参阅[设置部署属性 (Reporting Services)](tools/set-deployment-properties-reporting-services.md)。  
  
 可以使用 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 版本的 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 打开、修改、预览、保存和发布 [!INCLUDE[ssRSversion2005](../includes/ssrsversion2005-md.md)] 和 [!INCLUDE[ssRSversion10](../includes/ssrsversion10-md.md)] 报表。 有关详细信息，请参阅 [SQL Server Data Tools 中的部署和版本支持 (SSRS)](tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)中。  
  
### <a name="to-publish-all-reports-in-a-project"></a>发布项目中的所有报表  
  
-   在“生成”菜单中，单击“部署 **报表项目名称>”** **\<** 。 或者，在解决方案资源管理器中，右键单击报表项目，然后单击“部署”  。 可以在“输出”窗口中查看发布过程的状态。  
  
    > [!NOTE]  
    >  当您部署报表服务器项目时，也会部署报表服务器中的共享数据源。  
  
### <a name="to-publish-a-single-report"></a>发布单个报表  
  
-   在解决方案资源管理器中，右键单击报表，然后单击 **“部署”** 。 可以在“输出”窗口中查看发布过程的状态。  
  
    > [!NOTE]  
    >  当您发布报表时，还必须部署报表使用的共享数据源。  
  
## <a name="see-also"></a>另请参阅  
 [发布数据源和报表](reports/publishing-data-sources-and-reports.md)   
 [预览报表](reports/previewing-reports.md)   
 [将报表发布到报表服务器](reports/publishing-reports-to-a-report-server.md)   
 [查找、查看和管理报表（报表生成器和 SSRS）](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [导出报表 &#40;报表生成器和 SSRS&#41;](report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
