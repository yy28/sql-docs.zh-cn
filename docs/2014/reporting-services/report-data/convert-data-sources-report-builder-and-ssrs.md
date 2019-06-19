---
title: 转换从数据源嵌入到共享 （报表生成器和 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], embedded
- data sources [Reporting Services], shared
ms.assetid: 0e099c7e-8c03-43eb-9ea3-76e52d9ebbe3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 64879a7ab82f509f129cf43ab50c1cdbb3b7f913
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107412"
---
# <a name="convert-a-data-source-from-embedded-to-shared-report-builder-and-ssrs"></a>将嵌入数据源转换为共享数据源（报表生成器和 SSRS）
  “报表数据”窗格中的每个数据源都是嵌入且特定于报表的，或者是共享的。 在报表生成器中，共享数据源将指向报表服务器或 SharePoint 站点上的已发布共享数据源。 在报表设计器中，共享数据源将指向解决方案资源管理器中 **“共享数据源”** 文件夹下的某一共享数据源。  
  
 有关嵌入数据源与共享数据源之间的差异的详细信息，请参阅[嵌入和共享的数据连接或数据源（报表生成器和 SSRS）](../embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)。  
  
 有关如何创建共享数据源的详细信息，请参阅[创建嵌入或共享数据源 (SSRS)](../create-an-embedded-or-shared-data-source-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-designer"></a>报表设计器  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>将嵌入数据源转换为共享数据源  
  
-   在“报表数据”窗格中，右键单击数据源，然后单击“转换为共享数据源”  。  
  
    > [!NOTE]  
    >  如果“报表数据”窗格不可见，请单击 **“视图”** 菜单上的 **“报表数据”** 。 如果“报表数据”窗格以浮动窗口形式打开，则请停靠该窗格。 有关详细信息，请参阅[在报表设计器中停靠“报表数据”窗格 (SSRS)](../tools/dock-the-report-data-pane-in-report-designer-ssrs.md)。  
  
     在“报表数据”窗格中，数据源图标将更改为共享数据源图标。 在解决方案资源管理器中， **“共享数据源”** 文件夹中会出现一个同名的共享数据源。  
  
### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>将共享数据源转换为嵌入数据源  
  
-   在“报表数据”窗格中，右键单击数据源，打开“数据源属性”对话框，然后单击“嵌入连接”   。 输入必需的信息。  
  
     在“报表数据”窗格中，数据源图标将更改为共享数据源图标。  
  
## <a name="report-builder"></a>报表生成器  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>将嵌入数据源转换为共享数据源  
  
-   在“报表数据”窗格中，右键单击数据源以便打开“数据源属性”对话框，然后单击“嵌入连接”   。 输入必需的信息。  
  
     在“报表数据”窗格中，数据源图标将更改为共享数据源图标。  
  
#### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>将共享数据源转换为嵌入数据源  
  
-   在“报表数据”窗格中，右键单击数据源，打开“数据源属性”对话框，然后单击“嵌入连接”   。 输入必需的信息。  
  
     在“报表数据”窗格中，数据源图标将更改为共享数据源图标。  
  
## <a name="see-also"></a>请参阅  
 [管理报表数据源](manage-report-data-sources.md)   
 [报表生成器中的数据连接、数据源和连接字符串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)  
  
  
