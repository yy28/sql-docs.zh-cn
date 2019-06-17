---
title: 任务 5：从 Excel 中创建基于域的属性 |Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489109"
---
# <a name="task-5-creating-a-domain-based-attribute-from-excel"></a>任务 5：从 Excel 中创建基于域的属性
  在此任务中，您将转换**状态**的属性**供应商**作为实体**基于域的属性**。 配置基于域的一个，并将其发布到 MDS，名为的新实体的 State 属性之后**状态**将所有值位于列中的 MDS 服务器上创建并**状态**的属性**供应商**将使用中的值填充实体**状态**实体。 现在，**供应商**模型应具有两个实体：**供应商**并**状态**其中**状态**属性的**供应商**实体是一个基于域的属性，取决于**状态**实体。  
  
1.  切换到**Excel**具有窗口**Cleansed and Matched Suppliers.xlsx**打开。  
  
2.  单击**刷新**要从 MDS 获取最新的更新的功能区上的按钮。 如果您执行了可选，应看到两条详细记录**任务 4**。  
  
3.  单击列名称**状态**(单元格**I1**) 中**标头行**。  
  
     ![Excel-属性属性按钮](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-01.jpg "Excel-属性属性按钮")  
  
4.  单击**特性属性**功能区上。  
  
5.  在中**特性的属性**对话框中，选择**约束列表 （基于域的）** 有关**属性类型**。  
  
6.  类型**状态**有关**新实体名称**然后单击**确定**。  
  
     ![Excel-特性属性对话框](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-02.jpg "Excel-特性属性对话框")  
  
7.  现在，在 Excel 中，应看到**向下箭头**时单击中的任何值**状态**列。 可以根据需要使用下拉列表来更改该值。  
  
     ![Excel-下拉列表中与状态](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-03.jpg "Excel-下拉列表中与状态")  
  
## <a name="next-step"></a>下一步  
 [任务 6:验证使用主数据管理器创建基于域的属性](../../2014/tutorials/task-6-verify-domain-based-attribute-master-data-manager.md)  
  
  
