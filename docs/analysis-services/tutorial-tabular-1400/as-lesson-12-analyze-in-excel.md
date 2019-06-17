---
title: Analysis Services 教程第 12 课：在 Excel 中分析 |Microsoft Docs
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: c807825bfd4ef90491fb38e09e81eb79134fdbc9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62467792"
---
# <a name="analyze-in-excel"></a>在 Excel 中分析

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课中，您使用分析在 Excel 功能打开 Microsoft Excel、 自动创建到模型工作区中，连接并自动将数据透视表添加到工作表。 “在 Excel 中分析”功能旨在提供一种快速简便的方法，供您在部署模型之前测试模型设计的效用。 在本课程中不执行任何数据分析。 本课程的目的是让模型作者熟悉可用于测试模型设计的工具。   
  
若要完成本课程中，必须在与 Visual Studio 在同一台计算机上安装 Excel。
  
估计的时间才能完成本课程中：**5 分钟**  
  
## <a name="prerequisites"></a>先决条件  

本文是表格建模教程应按顺序完成的一部分。 执行任务之前在本课程中，您应当已完成上一课：[第 11 课：创建角色](../tutorial-tabular-1400/as-lesson-11-create-roles.md)。  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>使用默认透视和“Internet Sales”透视进行浏览  

在这些首要任务，使用默认透视，其中包括所有模型对象，浏览您的模型以及还通过使用 Internet 销售透视你之前创建。 “Internet Sales”透视将排除 Customer 表对象。  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>使用默认透视进行浏览  
  
1.  单击**模型**菜单 >**在 Excel 中的分析**。  
  
2.  在“在 Excel 中分析”  对话框中，单击“确定”  。  
  
    Excel 中打开新的工作簿。 将使用当前用户帐户创建一个数据源连接，默认透视将用于定义可查看字段。 数据透视表自动添加到工作表。  
  
3.  在 Excel 中，在**数据透视表字段列表**，请注意**DimDate**并**FactInternetSales**显示度量值组。 **DimCustomer**， **DimDate**， **DimGeography**， **DimProduct**， **DimProductCategory**，**DimProductSubcategory**，并**FactInternetSales**还显示具有各自的列的表。  
  
4.  关闭 Excel 而不保存工作簿。  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>使用“Internet Sales”透视进行浏览  
  
1.  单击**模型**菜单，并单击**在 Excel 中的分析**。  
  
2.  在“在 Excel 中分析”  对话框中，选中“当前 Windows 用户”  ，然后在“透视”  下拉列表框中，选中 **Internet Sales**，然后单击“确定”  。 
    
    ![as-lesson12-perspective](../tutorial-tabular-1400/media/as-lesson12-perspective.png)
    
3.  在 Excel 中，在**数据透视表字段**，请注意，从字段列表中排除 DimCustomer 表。  
    
    ![as-lesson12-fields](../tutorial-tabular-1400/media/as-lesson12-fields.png)
    
4.  关闭 Excel 而不保存工作簿。  
  
## <a name="browse-by-using-roles"></a>通过使用角色浏览  

角色是任何表格模型的一个重要部分。 如果没有向其用户作为成员添加至少一个角色，用户不能访问和使用您的模型分析数据。 “在 Excel 中分析”功能为您提供测试所定义的角色的方法。  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>若要浏览使用销售经理用户角色  
  
1.  在 SSDT 中，单击**模型**菜单，并单击**在 Excel 中的分析**。  
  
2.  在**指定的用户名或角色要用于连接到模型**，选择**角色**，然后在下拉列表框中，选择**销售经理**，然后单击**确定**。  
  
    Excel 中打开新的工作簿。 自动创建数据透视表。 数据透视表字段列表包括新模型中可用的所有数据字段。  
      
3.  关闭 Excel 而不保存工作簿。  
  
## <a name="whats-next"></a>下一步是什么？

请转到下一课：[第 13 课：部署](../tutorial-tabular-1400/as-lesson-13-deploy.md)。

  
  
  
