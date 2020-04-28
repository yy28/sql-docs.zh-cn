---
title: 任务16：验证主数据管理器 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 57ad9d3e-8f95-4df6-af01-c291ccf49164
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d9828c02625ae2bc5a85859577a237b4c4fa99c5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81484677"
---
# <a name="task-16-verifying-with-master-data-manager"></a>任务 16：使用主数据管理器进行验证
  在本任务中，您查看 SSIS 包所提交的批处理作业的状态并验证数据已使用主数据管理器上载到了 MDS 服务器。  
  
1.  启动**主数据管理器**（`http://localhost/MDS`）。 如果已打开，请单击顶部的 " **Microsoft SQL Server Master Data Services**切换到"**主页**"。  
  
2.  单击 "**集成管理**"。  
  
3.  请注意，在列表中有一个名为**EIMBatch**的批处理。 如果看不到以下屏幕，请单击菜单栏上的 "**导入数据**"。  
  
     ![EIM 批处理](../../2014/tutorials/media/et-verifyingwithmasterdatamanager.jpg "EIM 批处理")  
  
4.  单击顶部**SQL Server 2012 Master Data Services** ，切换回主页。  
  
5.  确保为 "**模型**" 选择 "**供应商**模型"，为 "**版本**" 选择 " **VERSION_1** "，然后单击 "**资源管理器**"。  
  
6.  您可以看到数据 SSIS 包已导入 MDS。 数据应为 "清理"，并且没有重复的**代码**值（注意： Excel 中的 "**供应商**" 列对应于 MDS 中的供应商实体的**Code**属性）。  
  
## <a name="next-step"></a>下一步  
 [任务 17：查看由 SSIS 包创建的 DQS 清理项目](../../2014/tutorials/task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package.md)  
  
  
