---
title: 第 12 课：在 Excel 中分析 |Microsoft Docs
ms.date: 08/22/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c42a45ec20edbde61a2f1b7c5b026f3467cd2371
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62468421"
---
# <a name="lesson-12-analyze-in-excel"></a>第 12 课：在 Excel 中分析
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在本课中，您将使用分析在 Excel 功能在 SSDT 中打开 Microsoft Excel、 自动创建的数据源连接到模型工作区，并自动将数据透视表添加到工作表。 “在 Excel 中分析”功能旨在提供一种快速简便的方法，供您在部署模型之前测试模型设计的效用。 在本课中，您将不执行任何数据分析。 本课程的目的是让模型作者熟悉可用于测试模型设计的工具。 与使用 Analyze in Excel 功能，这意味着模型作者，最终用户将使用客户端报告应用程序，如 Excel 或 Power BI 连接到并浏览部署的模型数据。  
  
若要完成本课程中，必须在 SSDT 所在的同一台计算机上安装 Excel。 若要了解详细信息，请参阅 [“在 Excel 中分析”](../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)安装在同一台计算机上。  
  
估计的时间才能完成本课程中：**20 分钟**  
  
## <a name="prerequisites"></a>先决条件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 执行任务之前在本课程中，您应当已完成上一课：[第 11 课：创建角色](../analysis-services/lesson-11-create-roles.md)。  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>使用默认透视和“Internet Sales”透视进行浏览  
在这些首要任务，您将浏览您的模型，通过使用这两个默认透视，其中包括所有模型对象，以及通过使用 Internet 销售透视你之前。 “Internet Sales”透视将排除 Customer 表对象。  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>使用默认透视进行浏览  
  
1.  单击**模型**菜单 >**在 Excel 中的分析**。  
  
2.  在“在 Excel 中分析”对话框中，单击“确定”。  
  
    Excel 将打开，并显示一个新工作簿。 将使用当前用户帐户创建一个数据源连接，默认透视将用于定义可查看字段。 数据透视表自动添加到工作表。  
  
3.  在 Excel 中，在**数据透视表字段列表**，请注意**DimDate**并**FactInternetSales**度量值组出现，并将**DimCustomer**， **DimDate**， **DimGeography**， **DimProduct**， **DimProductCategory**， **DimProductSubcategory**，并**FactInternetSales**及其各自的列的所有表的都显示。  
  
4.  关闭 Excel 而不保存工作簿。  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>使用“Internet Sales”透视进行浏览  
  
1.  单击**模型**菜单，并单击**在 Excel 中的分析**。  
  
2.  在“在 Excel 中分析”对话框中，选中“当前 Windows 用户”，然后在“透视”下拉列表框中，选中 **Internet Sales**，然后单击“确定”。 
    
    ![as-tabular-lesson12-perspective](../analysis-services/media/as-tabular-lesson12-perspective.png)
    
3.  在 Excel 中，在**数据透视表字段**，请注意，从字段列表中排除 DimCustomer 表。  
    
    ![as-tabular-lesson12-fields](../analysis-services/media/as-tabular-lesson12-fields.png)
    
4.  关闭 Excel 而不保存工作簿。  
  
## <a name="browse-by-using-roles"></a>通过使用角色浏览  
角色是任何表格模型中不可或缺的一部分。 如果没有向其用户作为成员添加至少一个角色，用户将不能访问和分析数据使用的模型。 “在 Excel 中分析”功能为您提供测试所定义的角色的方法。  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>若要浏览使用销售经理用户角色  
  
1.  在 SSDT 中，单击**模型**菜单，并单击**在 Excel 中的分析**。  
  
2.  在**在 Excel 中的分析**对话框中**指定的用户名或角色要用于连接到模型**，选择**角色**，然后在下拉列表框中，选择**销售经理**，然后单击**确定**。  
  
    Excel 将打开，并显示一个新工作簿。 自动创建数据透视表。 数据透视表字段列表包含您的新模型中提供的所有数据字段。  
      
3.  关闭 Excel 而不保存工作簿。  
  
## <a name="whats-next"></a>下一步是什么？
请转到下一课：[第 13 课：部署](../analysis-services/lesson-13-deploy.md)。

  
  
  
