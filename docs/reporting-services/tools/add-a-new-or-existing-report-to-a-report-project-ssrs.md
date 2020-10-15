---
title: 向报表项目中添加新报表或现有报表 | Microsoft Docs
description: 了解如何使用 SQL Server Reporting Services 中的报表向导向报表项目添加新报表或现有报表。
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], creating
ms.assetid: 8bc0bb53-ad8a-464d-bb6a-7fea5fa62c5c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 07d1f6d9f31fa300b2e9e43e80eda9c03111cc6c
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "91986503"
---
# <a name="add-a-new-or-existing-report-to-a-report-project-ssrs"></a>向报表项目中添加新报表或现有报表 (SSRS)
  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，你可以通过使用报表向导或通过将新的空白报表添加到项目中来添加新的 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 报表。 也可以添加现有报表。 添加报表后，您可以看到项目 **“报表”** 文件夹下会列出该报表名称。  
  
> [!NOTE]  
>  若要使用现有数据源预览报表，您必须有权从报表创作客户端访问此数据源。 有关详细信息，请参阅 [数据连接、数据源和连接字符串](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)。  
  
 添加报表后，您可以定义数据源和数据集，并且可以设计报表布局。 要开始使用，请参阅[创建基本表报表（SSRS 教程）](../../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)或[表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)。  
  
## <a name="to-add-a-new-report-using-the-report-wizard"></a>使用报表向导添加新报表  
  
1.  在解决方案资源管理器中，右键单击“报表”文件夹，然后单击“添加新报表”。 将打开 **“报表向导”** 对话框。  
  
     该向导将指导你逐步完成以下操作：创建数据源，创建带查询的数据集，定义组，指定布局，以及创建报表。 步骤包括：  
  
    -   **选择数据源。** 创建报表的第一步是定义数据源。 报表向导提供了报表项目中的所有共享数据源的列表，此外还提供了选项，用于创建新数据源。  
  
    -   **设计查询。** 第二步是设计查询。 您可以键入查询字符串，然后使用查询设计器生成它，也可以从另一个报表导入一个查询。 有关查询设计器的信息，请参阅 [Reporting Services Query Designers](/previous-versions/sql/)。  
  
    -   **选择报表类型。** 第三步是选择所需的报表类型。 您可以选择表格报表或矩阵报表。 表格报表的列数是固定的。 而矩阵报表（即交叉表报表）的列数根据查询结果而变化。 地图报表在地图背景下显示分析。  
  
    -   **为报表命名。**  最后一步是为报表命名并验证报表中将要包含的各个字段。 完成所有步骤之后，报表设计器将创建报表，并将其添加到报表服务器项目。  
  
## <a name="to-add-a-new-blank-report"></a>添加新的空白报表  
  
1.  在 **“项目”** 菜单上单击 **“添加新项”** 。  
  
2.  在 **“模板”** 上单击 **“报表”** 。  
  
3.  单击“添加”。  
  
     一个新的空白报表随即添加到项目中并显示在设计图面上。  
  
## <a name="to-add-an-existing-report"></a>添加现有报表  
  
1.  在“项目”  菜单上单击“添加” ，然后单击“现有项”  。  
  
2.  浏览到 .rdl 文件所在的位置并选择它，然后单击 **“添加”** 。  
  
     该报表随即添加到项目的 **“报表”** 文件夹下。 关闭并重新打开项目后，报表将按字母顺序排序。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 教程 (SSRS)](../../reporting-services/reporting-services-tutorials-ssrs.md)  
 更多疑问？ [请访问 Reporting Services 论坛](https://go.microsoft.com/fwlink/?LinkId=620231)
  
