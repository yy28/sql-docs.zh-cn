---
title: "第 13 课: 在 Excel 中分析 |Microsoft 文档"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: ce717071-193b-4c99-9654-c7a613e16327
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4c3fa27228e03c076eeb3800b21c34397b4c9834
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-12-analyze-in-excel"></a>在 Excel 中分析第 12 课：
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在本课程中，你将在 SSDT 中的 Excel 功能中使用分析以打开 Microsoft Excel、 自动创建数据源连接到模型工作区，并将数据透视表自动添加到工作表。 “在 Excel 中分析”功能旨在提供一种快速简便的方法，供您在部署模型之前测试模型设计的效用。 在本课中，您将不执行任何数据分析。 本课程的目的是让模型作者熟悉可用于测试模型设计的工具。 与不同 analyze in Excel 功能，目的为了的模型作者，最终用户将使用客户端报告应用程序，如 Excel 或 Power BI 连接到并浏览部署模型数据。  
  
若要完成本课程中，必须在 SSDT 所在的计算机上安装 Excel。 若要了解详细信息，请参阅 [“在 Excel 中分析”](../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)安装在同一台计算机上。  
  
学完本课的估计时间： **20 分钟**  
  
## <a name="prerequisites"></a>先决条件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 之前在本课程中执行任务，你应完成上一课：[课 11： 创建角色](../analysis-services/lesson-11-create-roles.md)。  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>使用默认透视和“Internet Sales”透视进行浏览  
在这些第一个任务，你将浏览你的模型，通过使用这两个默认透视，其中包括所有模型对象，以及通过使用 Internet Sales 透视你前面。 “Internet Sales”透视将排除 Customer 表对象。  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>使用默认透视进行浏览  
  
1.  单击**模型**菜单 >**在 Excel 中的分析**。  
  
2.  在“在 Excel 中分析”对话框中，单击“确定”。  
  
    Excel 将打开，并显示一个新工作簿。 将使用当前用户帐户创建一个数据源连接，默认透视将用于定义可查看字段。 数据透视表自动添加到工作表。  
  
3.  在 Excel 中，在**数据透视表字段列表**，请注意**DimDate**和**FactInternetSales**显示度量值组，以及**DimCustomer**， **DimDate**， **DimGeography**， **DimProduct**， **DimProductCategory**， **DimProductSubcategory**，和**FactInternetSales**所有各自的列的表会显示。  
  
4.  关闭 Excel 而不保存工作簿。  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>使用“Internet Sales”透视进行浏览  
  
1.  单击**模型**菜单，，然后单击**在 Excel 中的分析**。  
  
2.  在“在 Excel 中分析”对话框中，选中“当前 Windows 用户”，然后在“透视”下拉列表框中，选中 **Internet Sales**，然后单击“确定”。 
    
    ![作为-表格-lesson12-透视](../analysis-services/media/as-tabular-lesson12-perspective.png)
    
3.  在 Excel 中，在**数据透视表字段**，请注意从字段列表中排除 DimCustomer 表。  
    
    ![作为-表格-lesson12-字段](../analysis-services/media/as-tabular-lesson12-fields.png)
    
4.  关闭 Excel 而不保存工作簿。  
  
## <a name="browse-by-using-roles"></a>通过使用角色浏览  
角色是任何表格模型中不可或缺的一部分。 而无需向其添加用户作为成员的至少一个角色，用户将不能访问和使用你的模型分析数据。 “在 Excel 中分析”功能为您提供测试所定义的角色的方法。  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a>若要浏览使用销售经理用户角色  
  
1.  在 SSDT 中，单击**模型**菜单，，然后单击**在 Excel 中的分析**。  
  
2.  在**在 Excel 中的分析**对话框中，在**指定的用户名或角色要用于连接到模型**，选择**角色**，然后在下拉列表框中，选择**销售经理**，然后单击**确定**。  
  
    Excel 将打开，并显示一个新工作簿。 自动创建数据透视表。 数据透视表字段列表包含您的新模型中提供的所有数据字段。  
      
3.  关闭 Excel 而不保存工作簿。  
  
## <a name="whats-next"></a>下一步是什么？
转到下一课：[课 13： 部署](../analysis-services/lesson-13-deploy.md)。

  
  
  

