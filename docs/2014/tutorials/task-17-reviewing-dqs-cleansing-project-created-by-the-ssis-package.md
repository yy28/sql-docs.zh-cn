---
title: 任务17：查看由 SSIS 包创建的 DQS 清理项目 |Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "65484714"
---
# <a name="task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package"></a>任务 17：查看由 SSIS 包创建的 DQS 清理项目
  在该任务中，您将打开由 SSIS 包在 DQS 客户端中创建的 DQS 项目，检查清理过程的结果，并可选执行交互式清理和导出结果。  
  
1.  启动**Data Quality Client**。  
  
2.  单击 "**管理**" 窗格中的 "**活动监视**"。  
  
3.  根据**活动开始时间**对列表排序，以查看最新记录。  
  
4.  请注意，你会看到以下格式的项目名称： **cleanseandcurate.cleanse supplier data.guid**。  
  
     ![SSIS 包创建的 DQS 清理项目](../../2014/tutorials/media/et-reviewingdqscpcreatedbythessispackage.jpg "SSIS 包创建的 DQS 清理项目")  
  
5.  请注意，"**处于活动状态**" 字段中的值为 "**活动**"。  
  
6.  单击底部窗格中的 "**探查器**" 选项卡，查看 SSIS 包执行的清理活动的探查器统计信息。  
  
7.  单击 "**关闭**" 以关闭**管理**屏幕。  
  
8.  在**DQS 客户端**的主页中，单击 "**数据质量项目**" 窗格中的 "**打开数据质量项目**"。  
  
9. 在项目列表中，选择由 SSIS DQS 清理组件创建的项目。 项目的名称应采用以下格式： **cleanseandcurate.cleanse supplier data.guid （以红色表示）**。 您可能需要根据 "**创建日期**" 列对列表进行排序，并查找最新记录。  
  
10. 单击 **下一步**。  
  
11. 您在本教程前面部分的交互式清理中应熟悉 "**管理和查看结果**" 页。  
  
12. 查看清理结果。 在下一页中，您还可以执行交互式清理，并将结果导出到 Excel 文件或数据库中。  
  
13. 单击 **下一步**。 在此 "**导出**" 页中，您可以将结果导出到 excel 文件、CSV 文件或 SQL 数据库。  
  
14. 单击 "**完成**" 完成活动。  
  
15. 在**DQS 客户端**的主页中，单击 "**管理**" 窗格中的 "**活动监视**"。  
  
16. 请注意，项目的**IsActive**字段值现在**结束**。  
  
## <a name="next-step"></a>下一步  
 [结束语](../../2014/tutorials/conclusion.md)  
  
  
