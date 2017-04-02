---
title: "第 14 课：部署 | Microsoft Docs"
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
ms.assetid: 24863a8a-9017-415a-a97b-fbac76ed0675
caps.latest.revision: 25
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# 第 14 课：部署
在本课中，您将配置部署属性；同时指定在表格模式下运行的 Analysis Services 的部署服务器实例以及为您要部署的模型指定名称。 然后，将模型部署到该实例。 部署此模型之后，用户可以使用报表客户端应用程序连接到该模型。 若要了解详细信息，请参阅[表格模型解决方案部署（SSAS 表格）](../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)。  
  
学完本课的估计时间：**5 分钟**  
  
## 先决条件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 在执行本课程中的任务之前，应该已完成上一课：[第 13 课：在 Excel 中分析](../analysis-services/lesson-13-analyze-in-excel.md)。  
  
## 部署模型  
  
#### 配置部署属性  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 的“解决方案资源管理器”中，右键单击“Adventure Works Internet Sales Tabular Model”项目，然后在上下文菜单中单击“属性”。  
  
2.  在“AW Internet Sales Tabular Model 属性页”对话框中，在“部署服务器”下的“服务器”属性中，键入在表格模式下运行的 Analysis Services 实例的名称。 这将是您的模型将被部署到的实例。  
  
    > [!IMPORTANT]  
    > 您必须对远程 Analysis Services 实例具有管理员权限，才能将模型部署到该实例。  
  
3.  在“数据库”属性中，键入 **Adventure Works Internet Sales Model**。  
  
4.  在“多维数据集名称”属性中，键入 **Adventure Works Internet Sales Model**。  
  
5.  验证所做的选择，然后单击“确定”。  
  
#### 部署 Adventure Works Internet Sales 表格模型  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，单击“生成”菜单，然后单击“部署 AW Internet Sales Tabular Model”。  
  
    “部署”对话框将出现，并且显示模型中包括的元数据和每个表的部署状态。  
  
2. 成功完成部署后，继续操作并单击“关闭”。  
  
## 结语  
恭喜！ 已完成创作和部署第一个 Analysis Services 表格模型的过程。 本教程已帮助指导您完成了创建表格模型的最常见任务。 既然已部署了 Adventure Works Internet Sales Model，就可以使用 SQL Server Management Studio 来管理此模型、创建进程脚本和备份计划。 用户可以使用报表客户端应用程序（如 Microsoft Excel 或 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]）连接到此模型。  
  
## 其他资源  
若要了解有关支持 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 报表的表格模型属性的详细信息，请参阅 [Power View 报表属性（SSAS 表格）](../analysis-services/tabular-models/power-view-reporting-properties-ssas-tabular.md)。  
  
## 另请参阅  
[DirectQuery 模式（SSAS 表格）](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)  
[配置默认数据建模和部署属性（SSAS 表格）](../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)  
[表格模型数据库（SSAS 表格）](../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)  
  
  
  
