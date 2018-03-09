---
title: "转换数据源（报表生成器和 SSRS）| Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [Reporting Services], embedded
- data sources [Reporting Services], shared
ms.assetid: 0e099c7e-8c03-43eb-9ea3-76e52d9ebbe3
caps.latest.revision: "16"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b2bf27f67645387e78806cddf7fc195d0d4904ef
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="convert-data-sources-report-builder-and-ssrs"></a>转换数据源（报表生成器和 SSRS）
  “报表数据”窗格中的每个数据源都是嵌入且特定于报表的，或者是共享的。 在报表生成器中，共享数据源将指向报表服务器或 SharePoint 站点上的已发布共享数据源。 在报表设计器中，共享数据源将指向解决方案资源管理器中 **“共享数据源”** 文件夹下的某一共享数据源。  
  
 有关嵌入数据源与共享数据源之间的差异的详细信息，请参阅[嵌入和共享的数据连接或数据源（报表生成器和 SSRS）](http://msdn.microsoft.com/library/f417782c-b85a-4c4d-8a40-839176daba56)。  
  
 有关如何创建共享数据源的详细信息，请参阅[创建嵌入或共享数据源 (SSRS)](http://msdn.microsoft.com/library/b111a8d0-a60d-4c8b-b00a-51644b19c34b)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-designer"></a>报表设计器  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>将嵌入数据源转换为共享数据源  
  
-   在“报表数据”窗格中，右键单击数据源，然后单击“转换为共享数据源”。  
  
    > [!NOTE]  
    >  如果“报表数据”窗格不可见，请单击 **“视图”** 菜单上的 **“报表数据”**。 如果“报表数据”窗格以浮动窗口形式打开，则请停靠该窗格。 有关详细信息，请参阅[在报表设计器中停靠“报表数据”窗格 (SSRS)](../../reporting-services/tools/dock-the-report-data-pane-in-report-designer-ssrs.md)。  
  
     在“报表数据”窗格中，数据源图标将更改为共享数据源图标。 在解决方案资源管理器中， **“共享数据源”** 文件夹中会出现一个同名的共享数据源。  
  
### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>将共享数据源转换为嵌入数据源  
  
-   在“报表数据”窗格中，右键单击数据源，打开“数据源属性”对话框，然后单击“嵌入连接”。 输入必需的信息。  
  
     在“报表数据”窗格中，数据源图标将更改为共享数据源图标。  
  
## <a name="report-builder"></a>报表生成器  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>将嵌入数据源转换为共享数据源  
  
-   在“报表数据”窗格中，右键单击数据源以便打开“数据源属性”对话框，然后单击“嵌入连接”。 输入必需的信息。  
  
     在“报表数据”窗格中，数据源图标将更改为共享数据源图标。  
  
#### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>将共享数据源转换为嵌入数据源  
  
-   在“报表数据”窗格中，右键单击数据源，打开“数据源属性”对话框，然后单击“嵌入连接”。 输入必需的信息。  
  
     在“报表数据”窗格中，数据源图标将更改为共享数据源图标。  
  
## <a name="see-also"></a>另请参阅  
 [管理报表数据源](../../reporting-services/report-data/manage-report-data-sources.md)   
 [数据连接、数据源和连接字符串（报表生成器和 SSRS）](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
