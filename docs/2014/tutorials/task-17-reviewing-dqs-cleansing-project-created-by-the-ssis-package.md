---
title: 任务 17：查看由 SSIS 包的项目创建的 DQS 清理 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: fc6cc258-72f5-4593-8edb-9f5bc66de9db
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 285eae7ea20d5919fa73bd0d514c755fe73d9de0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65484714"
---
# <a name="task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package"></a>任务 17：查看由 SSIS 包创建的 DQS 清理项目
  在该任务中，您将打开由 SSIS 包在 DQS 客户端中创建的 DQS 项目，检查清理过程的结果，并可选执行交互式清理和导出结果。  
  
1.  启动**数据质量客户端**。  
  
2.  单击**活动监视**中**管理**窗格。  
  
3.  对基于列表进行排序**活动开始时间**若要查看最新记录。  
  
4.  请注意，您将看到采用以下格式的项目的名称：**CleanseAndCurate.Cleanse Supplier Data.GUID**。  
  
     ![DQS 清理项目创建的 SSIS 包](../../2014/tutorials/media/et-reviewingdqscpcreatedbythessispackage.jpg "DQS 清理项目创建的 SSIS 包")  
  
5.  请注意，中的值**是活动**字段是**Active**。  
  
6.  单击**Profiler**中底部窗格中，若要查看的清理活动的 SSIS 包执行的探查器统计信息选项卡。  
  
7.  单击**关闭**以关闭**管理**屏幕。  
  
8.  在主页面中的**DQS 客户端**，单击**打开数据质量项目**中**数据质量项目**窗格。  
  
9. 在项目列表中，选择由 SSIS DQS 清理组件创建的项目。 项目的名称应采用格式：**CleanseAndCurate.Cleanse Supplier Data.GUID (红色）** 。 可能需要对基于列表进行排序**创建日期**列，并寻找最新记录。  
  
10. 单击“下一步”  。  
  
11. **管理和查看结果**页应非常熟悉交互式清理在本教程前面部分中一样。  
  
12. 查看清理结果。 在下一页中，您还可以执行交互式清理，并将结果导出到 Excel 文件或数据库中。  
  
13. 单击“下一步”  。 在此**导出**页上，您可以将结果导出到 excel 文件，CSV 文件或 SQL 数据库。  
  
14. 单击**完成**以完成活动。  
  
15. 在主页面中的**DQS 客户端**，单击**活动监视**中**管理**窗格。  
  
16. 请注意，值**IsActive**字段为项目**已结束**现在。  
  
## <a name="next-step"></a>下一步  
 [结语](../../2014/tutorials/conclusion.md)  
  
  
