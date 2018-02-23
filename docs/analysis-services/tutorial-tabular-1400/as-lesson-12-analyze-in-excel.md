---
title: "Analysis Services 教程课 12： 在 Excel 中分析 |Microsoft 文档"
description: "描述如何在 Analysis Services tutorial 项目中，在 Excel 中使用分析。"
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
ms.openlocfilehash: dda8a42cd5e82c60f98de8ab351274f3c1e93820
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2018
---
# <a name="analyze-in-excel"></a>在 Excel 中分析

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课程中，分析功能中使用 Excel 打开 Microsoft Excel、 自动创建到模型工作区中，连接和自动向工作表中添加一个数据透视表。 “在 Excel 中分析”功能旨在提供一种快速简便的方法，供您在部署模型之前测试模型设计的效用。 在本课程中不执行任何数据分析。 本课程的目的是让模型作者熟悉可用于测试模型设计的工具。   
  
若要完成本课程中，必须在与 Visual Studio 在同一台计算机上安装 Excel。
  
学完本课的估计时间： **5 分钟**  
  
## <a name="prerequisites"></a>必要條件  

本文摘自表格建模教程中，应按顺序完成。 之前在本课程中执行任务，你应完成上一课：[课 11： 创建角色](../tutorial-tabular-1400/as-lesson-11-create-roles.md)。  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>使用默认透视和“Internet Sales”透视进行浏览  

这些第一个任务，在你浏览您的模型通过使用这两个默认透视，其中包括所有模型对象，以及通过使用 Internet Sales 透视你前面。 “Internet Sales”透视将排除 Customer 表对象。  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>使用默认透视进行浏览  
  
1.  单击**模型**菜单 >**在 Excel 中的分析**。  
  
2.  在“在 Excel 中分析”对话框中，单击“确定”。  
  
    Excel 将打开与新的工作簿。 将使用当前用户帐户创建一个数据源连接，默认透视将用于定义可查看字段。 数据透视表自动添加到工作表。  
  
3.  在 Excel 中，在**数据透视表字段列表**，请注意**DimDate**和**FactInternetSales**度量值组显示。 **DimCustomer**， **DimDate**， **DimGeography**， **DimProduct**， **DimProductCategory**， **DimProductSubcategory**，和**FactInternetSales**具有各自的列的表还显示。  
  
4.  关闭 Excel 而不保存工作簿。  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>使用“Internet Sales”透视进行浏览  
  
1.  单击**模型**菜单，，然后单击**在 Excel 中的分析**。  
  
2.  在“在 Excel 中分析”对话框中，选中“当前 Windows 用户”，然后在“透视”下拉列表框中，选中 **Internet Sales**，然后单击“确定”。 
    
    ![as-lesson12-perspective](../tutorial-tabular-1400/media/as-lesson12-perspective.png)
    
3.  在 Excel 中，在**数据透视表字段**，请注意从字段列表中排除 DimCustomer 表。  
    
    ![as-lesson12-fields](../tutorial-tabular-1400/media/as-lesson12-fields.png)
    
4.  关闭 Excel 而不保存工作簿。  
  
## <a name="browse-by-using-roles"></a>通过使用角色浏览  

角色是任何表格模型的一个重要部分。 用户将添加为成员的至少一个角色，用户无法访问而无需使用你的模型分析数据。 “在 Excel 中分析”功能为您提供测试所定义的角色的方法。  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>若要浏览使用销售经理用户角色  
  
1.  在 SSDT 中，单击**模型**菜单，，然后单击**在 Excel 中的分析**。  
  
2.  在**指定的用户名或角色要用于连接到模型**，选择**角色**，然后在下拉列表框中，选择**销售经理**，然后单击**确定**。  
  
    Excel 将打开与新的工作簿。 自动创建数据透视表。 数据透视表字段列表包括在你的新模型中可用的所有数据字段。  
      
3.  关闭 Excel 而不保存工作簿。  
  
## <a name="whats-next"></a>下一步是什么？

转到下一课：[课 13： 部署](../tutorial-tabular-1400/as-lesson-13-deploy.md)。

  
  
  
