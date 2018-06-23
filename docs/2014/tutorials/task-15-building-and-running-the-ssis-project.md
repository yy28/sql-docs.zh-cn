---
title: 任务 15： 生成并运行 SSIS 项目，|Microsoft 文档
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
ms.assetid: 13adf4e0-216a-4992-b13d-b7b1e1629e77
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9a63fcf03591626d5b4c1351d5ce868ef7a9fb65
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026243"
---
# <a name="task-15-building-and-running-the-ssis-project"></a>任务 15：生成和运行 SSIS 项目
  在本任务中，您将生成并运行 SSIS 项目。 如果必须在计算机上安装 Excel 2010 的 64 位版本，你应将的值设置**Run64BitRuntime**到**False** Excel 源工作。  
  
1.  在**解决方案资源管理器**窗口中，单击**项目**上菜单，然后单击**CleanseAndCurateSuppliers 属性**。  
  
2.  在**属性**对话框框中，展开**配置属性**左侧，然后单击**调试**。  
  
3.  设置**Run64BitRuntime**到**False**。  
  
     ![CleanseAndCurateSuppliers 项目属性](../../2014/tutorials/media/et-buildingandrunningthessisproject-01.jpg "CleanseAndCurateSuppliers 项目属性")  
  
4.  单击**确定**关闭**属性**对话框。  
  
5.  单击**生成**菜单栏，单击**生成 CleanseAndCurateSuppliers**。 确保没有生成错误。  
  
6.  单击**调试**单击菜单栏上**启动调试**。  
  
7.  查看中的消息**进度**窗口，并验证该包执行和成功结束。  
  
     ![通过进度窗口结果](../../2014/tutorials/media/et-buildingandrunningthessisproject-02.jpg "结果从进度窗口")  
  
     ![从进度窗口的最终状态](../../2014/tutorials/media/et-buildingandrunningthessisproject-03.jpg "进度窗口中的最终状态")  
  
8.  单击**调试**菜单栏，单击**停止调试**以停止调试会话。 如果包失败，应启用数据查看器并查看数据在组件之间的流动方式。  
  
## <a name="next-step"></a>下一步  
 [任务 16：使用主数据管理器进行验证](../../2014/tutorials/task-16-verifying-with-master-data-manager.md)  
  
  