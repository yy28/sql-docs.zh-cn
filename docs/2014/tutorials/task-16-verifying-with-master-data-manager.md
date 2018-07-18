---
title: 任务 16： 验证使用主数据管理器 |Microsoft Docs
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
ms.topic: conceptual
ms.assetid: 57ad9d3e-8f95-4df6-af01-c291ccf49164
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7d0c5b2f72a04b1c1f99829e61ca2dca3fedc39a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304643"
---
# <a name="task-16-verifying-with-master-data-manager"></a>任务 16：使用主数据管理器进行验证
  在本任务中，您查看 SSIS 包所提交的批处理作业的状态并验证数据已使用主数据管理器上载到了 MDS 服务器。  
  
1.  启动**主数据管理器**([http://localhost/MDS](http://localhost/MDS))。 如果已打开，请单击**Microsoft SQL Server Master Data Services**顶部以切换到**主页**。  
  
2.  单击**集成管理**。  
  
3.  请注意，没有与批处理名为**EIMBatch**提交列表中。 单击**导入数据**如果您看不到以下屏幕的菜单栏上。  
  
     ![EIM 批处理](../../2014/tutorials/media/et-verifyingwithmasterdatamanager.jpg "EIM 批处理")  
  
4.  切换回主页上单击**SQL Server 2012 Master Data Services**顶部。  
  
5.  请确保**供应商**为选择模型**模型**并**VERSION_1**为选择**版本**，然后单击**资源管理器**。  
  
6.  您可以看到数据 SSIS 包已导入 MDS。 数据应已清理，没有重复**代码**值 (注意： **SupplierID**在 Excel 中的列对应于**代码**MDS 中 Supplier 实体的属性)。  
  
## <a name="next-step"></a>下一步  
 [任务 17：查看由 SSIS 包创建的 DQS 清理项目](../../2014/tutorials/task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package.md)  
  
  
