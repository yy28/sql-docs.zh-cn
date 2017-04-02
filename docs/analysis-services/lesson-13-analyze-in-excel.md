---
title: "第 13 课：在 Excel 中分析 | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: ce717071-193b-4c99-9654-c7a613e16327
caps.latest.revision: 22
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 第 13 课：在 Excel 中分析
在本课中，您将使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中的“在 Excel 中分析”功能打开 Microsoft Excel、自动创建到模型工作区的数据源连接以及自动将数据透视表添加到工作表。 “在 Excel 中分析”功能旨在提供一种快速简便的方法，供您在部署模型之前测试模型设计的效用。 在本课中，您将不执行任何数据分析。 本课程的目的是让模型作者熟悉可用于测试模型设计的工具。 与模型作者使用“在 Excel 中分析”功能所不同的是，最终用户将使用客户端报告应用程序（如 Excel 或 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]）来连接和浏览部署的模型数据。  
  
为了完成此课程，Excel 必须与 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 安装在同一台计算机上。 若要了解详细信息，请参阅[在 Excel 中分析（SSAS 表格）](../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)。  
  
学完本课的估计时间：**20 分钟**  
  
## 先决条件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 在执行本课程中的任务之前，须已完成上一课：[第 11 课：创建分区](../analysis-services/lesson-11-create-partitions.md)。  
  
## 使用默认透视和“Internet Sales”透视进行浏览  
在第一批任务中，您将使用默认透视（包含所有模型对象）和您在第 8 课“创建透视”中创建的“Internet Sales”透视来浏览您的模型。 “Internet Sales”透视将排除 Customer 表对象。  
  
#### 使用默认透视进行浏览  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，单击 **“模型”** 菜单，然后单击 **“在 Excel 中分析”**。  
  
2.  在“在 Excel 中分析”对话框中，单击“确定”。  
  
    Excel 将打开，并显示一个新工作簿。 将使用当前用户帐户创建一个数据源连接，默认透视将用于定义可查看字段。 数据透视表将自动添加到工作表中。  
  
3.  在 Excel 的“数据透视表字段列表”中，请注意，将显示 **Date** 和 **Internet Sales** 度量值组，并且将显示 **Customer**、**Date**、**Geography**、**Product**、**Product Category**、**Product Subcategory**和 **Internet Sales** 表及其所有透视列。  
  
4.  关闭 Excel 而不保存工作簿。  
  
#### 使用“Internet Sales”透视进行浏览  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，单击 **“模型”** 菜单，然后单击 **“在 Excel 中分析”**。  
  
2.  在“在 Excel 中分析”对话框中，选中“当前 Windows 用户”，然后在“透视”下拉列表框中，选中 **Internet Sales**，然后单击“确定”。 Excel 将打开。  
  
3.  在 Excel 的“数据透视表字段列表”中，请注意 Customer 表已从字段列表中排除。  
  
4.  关闭 Excel 而不保存工作簿。  
  
## 使用角色进行浏览  
角色是任何表格模型中不可或缺的一部分。 一个角色都没有（用户可以作为成员添加到这些角色），用户将不能使用您的模型访问和分析数据。 “在 Excel 中分析”功能为您提供测试所定义的角色的方法。  
  
#### 使用“Internet Sales Manager”用户角色进行浏览  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，单击 **“模型”** 菜单，然后单击 **“在 Excel 中分析”**。  
  
2.  在“在 Excel 中分析”对话框的“指定要用于连接到模型的用户名或角色”中，选中“角色”，然后在下拉列表框中，选中 **Internet Sales Manager**，然后单击“确定”。  
  
    Excel 将打开，并显示一个新工作簿。 将自动创建一个数据透视表。 数据透视表字段列表包含您的新模型中提供的所有数据字段。  
      
3.  关闭 Excel 而不保存工作簿。  
  
## 后续步骤  
要继续学习本教程，请转到下一课：[第 14 课：部署](../analysis-services/lesson-14-deploy.md)。  
  
  
  
