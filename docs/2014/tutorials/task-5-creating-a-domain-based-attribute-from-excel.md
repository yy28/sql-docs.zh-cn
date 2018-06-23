---
title: 任务 5： 从 Excel 中创建基于域的属性 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 07cbc624-2c6b-4568-96e4-f18663a05d80
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 5e7a8dda16d8f513b2c4b07b9f41712be806b8a9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123521"
---
# <a name="task-5-creating-a-domain-based-attribute-from-excel"></a>任务 5：从 Excel 中创建基于域的属性
  在此任务中，你将转换**状态**属性**供应商**作为实体**基于域的属性**。 配置状态属性是基于域的一个，并将其发布到 MDS，名为的新实体后**状态**将列中的所有值 MDS 服务器上创建和**状态**的属性**供应商**将中的值填充实体**状态**实体。 现在，**供应商**模型应具有两个实体：**供应商**和**状态**其中**状态**属性**供应商**实体是一种基于域的特性，取决于**状态**实体。  
  
1.  切换到**Excel**窗口具有**Cleansed 和匹配 Suppliers.xlsx**打开。  
  
2.  单击**刷新**要从 MDS 中获取最新的更新的功能区上的按钮。 如果你已执行可选应会看到两个更多记录**任务 4**。  
  
3.  单击列名称**状态**(单元格**I1**) 中**标头行**。  
  
     ![Excel-属性属性按钮](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-01.jpg "Excel-属性属性按钮")  
  
4.  单击**特性属性**功能区上。  
  
5.  在**特性属性**对话框中，选择**Constrained 列表 （基于域的）** 为**属性类型**。  
  
6.  类型**状态**为**新的实体名称**单击**确定**。  
  
     ![Excel-属性属性对话框](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-02.jpg "Excel-属性属性对话框")  
  
7.  现在，在 Excel 中，你应看到**向下箭头**单击中的任何值**状态**列。 可以根据需要使用下拉列表来更改该值。  
  
     ![Excel-下拉列表中包含状态](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-03.jpg "Excel-下拉列表，其中包含的状态")  
  
## <a name="next-step"></a>下一步  
 [任务 6：验证通过使用主数据管理器创建了基于域的属性](../../2014/tutorials/task-6-verify-domain-based-attribute-master-data-manager.md)  
  
  