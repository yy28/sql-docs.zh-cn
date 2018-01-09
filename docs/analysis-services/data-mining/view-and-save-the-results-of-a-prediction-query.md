---
title: "查看和保存预测查询的结果 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- prediction queries [Analysis Services]
- viewing prediction query results
- displaying prediction query results
- Mining Model Prediction [Analysis Services], viewing results
ms.assetid: abba4d24-3619-44c1-8279-88f27ad627d3
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a96b6825f5b7b5d83981f6c0ec73e8020169b2b7
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="view-and-save-the-results-of-a-prediction-query"></a>查看和保存预测查询的结果
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]在定义中的某个查询后[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]通过使用预测查询生成器，可以运行查询，并通过切换到查询结果视图中查看结果。  
  
 可以将预测查询的结果保存到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目中定义的任何数据源的表中。 可以创建新的表，也可以将查询结果保存到现有表中。 如果将结果保存到现有表中，可以选择覆盖表中当前存储的数据；否则，查询结果将追加到表中现有数据的末尾。  
  
### <a name="run-a-query-and-view-the-results"></a>运行查询并查看结果  
  
1.  在 **的数据挖掘设计器中，单击** “挖掘模型预测” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]选项卡工具栏上的 **“结果”** 。  
  
     此时将打开查询结果视图并运行查询。 结果显示在查看器的网格中。  
  
### <a name="save-the-results-of-a-prediction-query-to-a-table"></a>将预测查询的结果保存到表  
  
1.  在数据挖掘设计器中，同 **“挖掘模型预测”** 选项卡工具栏上的 **“保存查询结果”**。  
  
     此时将打开 **“保存数据挖掘查询结果”** 对话框。  
  
2.  从 **“数据源”** 列表中选择数据源，或单击 **“新建”** 创建新的数据源。  
  
3.  在 **“表名称”** 框中，输入表的名称。 如果表已经存在，选择 **“如果已存在，则覆盖”** ，则可用查询结果替换表的内容。 如果不希望覆盖表的内容，请不要选中此复选框。 新的查询结果将追加到表中现有数据的末尾。  
  
4.  如果希望将表添加到数据源视图中，请从 **“添加到数据源视图”** 中选择数据源视图。  
  
5.  单击 **“保存”**。  
  
    > [!WARNING]  
    >  如果目标不支持分层行集，则可以向结果中添加 FALTTENED 关键字以另存为平面表。  
  
  
