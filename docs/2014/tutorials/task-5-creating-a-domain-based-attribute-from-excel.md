---
title: 任务5：从 Excel 中创建基于域的属性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 07cbc624-2c6b-4568-96e4-f18663a05d80
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f7e88065ff66ea953d0a91ed080fc3d7159ab794
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "65489109"
---
# <a name="task-5-creating-a-domain-based-attribute-from-excel"></a>任务 5：从 Excel 中创建基于域的属性
  在此任务中，您将**供应商**实体的**State**属性转换为**基于域的属性**。 将状态属性配置为基于域的属性并将其发布到 MDS 后，将在 MDS 服务器上创建一个名为 "**状态**" 的新实体，其中包含列中的所有值，并使用 "**状态**" 实体中的值填充 "**供应商**" 实体的 "**状态**" 属性。 现在，**供应**商模型应具有两个实体 **：供应商和****州**，其中**供应商**实体的**state**属性是依赖于**州**实体的基于域的属性。  
  
1.  切换到**清理和匹配的供应商 .xlsx**的**Excel**窗口。  
  
2.  单击功能区上的 "**刷新**" 按钮可从 MDS 获取最新更新。 如果执行了可选**任务 4**，则应该会看到另外两个记录。  
  
3.  单击**标题行**中的 "列名**状态**（单元格**I1**）"。  
  
     ![Excel -“特性”属性按钮](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-01.jpg "Excel -“特性”属性按钮")  
  
4.  在功能区上单击 "**特性属性**"。  
  
5.  在 "**特性属性**" 对话框中，选择 "**约束列表（基于域）** " 作为**属性类型**。  
  
6.  键入**新实体名称**的**状态**，然后单击 **"确定"**。  
  
     ![Excel -“特性”属性对话框](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-02.jpg "Excel -“特性”属性对话框")  
  
7.  现在，在 Excel 中，单击 "**状态**" 列中的任何值时，应会看到**向下箭头**。 可以根据需要使用下拉列表来更改该值。  
  
     ![Excel - 带州/省的下拉列表](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-03.jpg "Excel - 带州/省的下拉列表")  
  
## <a name="next-step"></a>下一步  
 [任务 6：验证基于域的属性是否使用主数据管理器进行创建](../../2014/tutorials/task-6-verify-domain-based-attribute-master-data-manager.md)  
  
  
