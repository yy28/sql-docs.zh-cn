---
title: 任务 10： 配置要使用引用数据服务的复合域 |Microsoft 文档
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 752eefde-8b87-4f54-878e-9963ccbadc8e
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 2a5d37578ac8336b67201161ef4de59baf90649c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018759"
---
# <a name="task-10-configuring-composite-domain-to-use-reference-data-service"></a>任务 10：配置复合域以使用引用数据服务
  在此任务中，你配置**地址验证**要使用的复合域**Melissa Data – 地址检查**服务。 在运行时，在清理活动期间，DQS 将“地址验证”域中各域的值传递给此服务以进行清理。 请参阅[映射到引用数据的域/复合域](http://msdn.microsoft.com/library/hh213030.aspx)有关详细信息。  
  
1.  在主页面中的**DQS 客户端**，单击**供应商 （域管理）** 下**最近的知识库**以启动**域管理**页。  
  
2.  选择**地址验证**复合域中的**的域列表**。  
  
3.  在右窗格中，切换到**引用数据**选项卡。  
  
     ![引用数据选项卡](../../2014/tutorials/media/et-configuringcdtouserds-01.jpg "引用数据选项卡")  
  
4.  单击**浏览**工具栏上的按钮。  
  
5.  上**联机引用数据提供程序目录**对话框中，选择**复选框**旁边**Melissa Data – 地址检查**。  
  
     ![选择 Melissa Data-地址检查](../../2014/tutorials/media/et-configuringcdtouserds-02.jpg "选择 Melissa Data-地址检查")  
  
6.  在右窗格中，在**架构**部分中，映射**地址行**域指向**地址行 (M)** 使用下拉列表的架构项。  
  
     ![映射到域的 RDS 架构项](../../2014/tutorials/media/et-configuringcdtouserds-03.jpg "RDS 架构项映射到域")  
  
7.  单击**添加架构项 （+）** 工具栏上的按钮在列表中创建条目。  
  
     ![添加架构项工具栏按钮](../../2014/tutorials/media/et-configuringcdtouserds-04.jpg "添加架构项工具栏按钮")  
  
8.  通过使用下图中所示的下拉列表，映射以下 DQS 域。  
  
     ![将 RDS 架构项映射到域](../../2014/tutorials/media/et-configuringcdtouserds-05.jpg "将 RDS 架构项映射到域")  
  
9. 单击 **“确定”** 关闭对话框。  
  
## <a name="next-step"></a>下一步  
 [任务 11：发布知识库](../../2014/tutorials/task-11-publishing-the-knowledge-base.md)  
  
  