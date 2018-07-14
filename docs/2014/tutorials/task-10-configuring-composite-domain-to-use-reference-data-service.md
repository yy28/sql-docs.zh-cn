---
title: 任务 10： 配置复合域以使用引用数据服务 |Microsoft Docs
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
ms.topic: conceptual
ms.assetid: 752eefde-8b87-4f54-878e-9963ccbadc8e
caps.latest.revision: 8
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5abc5bc02b2c7ee365886ba54a603890c4b2aa0f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37228343"
---
# <a name="task-10-configuring-composite-domain-to-use-reference-data-service"></a>任务 10：配置复合域以使用引用数据服务
  在此任务中，配置**地址验证**复合域以使用**Melissa Data – Address Check**服务。 在运行时，在清理活动期间，DQS 将“地址验证”域中各域的值传递给此服务以进行清理。 请参阅[映射到引用数据的域/复合域](http://msdn.microsoft.com/library/hh213030.aspx)的更多详细信息。  
  
1.  在主页面中的**DQS 客户端**，单击**Suppliers （域管理）** 下**最近的知识库**以启动**域管理**页。  
  
2.  选择**地址验证**复合域**的域列表**。  
  
3.  在右窗格中，切换到**引用数据**选项卡。  
  
     ![引用数据选项卡](../../2014/tutorials/media/et-configuringcdtouserds-01.jpg "引用数据选项卡")  
  
4.  单击**浏览**工具栏上的按钮。  
  
5.  上**Online Reference Data Providers Catalog**对话框中，选择**复选框**旁边**Melissa Data – Address Check**。  
  
     ![选择 Melissa 数据-地址检查](../../2014/tutorials/media/et-configuringcdtouserds-02.jpg "选择 Melissa 数据-地址检查")  
  
6.  在右窗格中，在**架构**部分中，将**Address Line**域**地址行 (M)** 架构项，通过使用下拉列表。  
  
     ![将 RDS 架构项映射到域](../../2014/tutorials/media/et-configuringcdtouserds-03.jpg "将 RDS 架构项映射到域")  
  
7.  单击**添加架构项 （+）** 按钮在工具栏上，若要在列表中创建一个条目。  
  
     ![添加架构项工具栏按钮](../../2014/tutorials/media/et-configuringcdtouserds-04.jpg "添加架构项工具栏按钮")  
  
8.  通过使用下图中所示的下拉列表，映射以下 DQS 域。  
  
     ![将 RDS 架构项映射到域](../../2014/tutorials/media/et-configuringcdtouserds-05.jpg "将 RDS 架构项映射到域")  
  
9. 单击 **“确定”** 关闭对话框。  
  
## <a name="next-step"></a>下一步  
 [任务 11：发布知识库](../../2014/tutorials/task-11-publishing-the-knowledge-base.md)  
  
  
