---
title: 任务 15：生成和运行 SSIS 项目 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 13adf4e0-216a-4992-b13d-b7b1e1629e77
ms.author: lle
author: lrtoyou1223
ms.openlocfilehash: 50b313f63ae434a96d6c0e38f3c8b600914c806d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66822995"
---
# <a name="task-15-building-and-running-the-ssis-project"></a>任务 15：生成和运行 SSIS 项目

  在本任务中，您将生成并运行 SSIS 项目。 如果必须在计算机上安装 Excel 2010 的 64 位版本，则应设置的值**Run64BitRuntime**到**False**有关 Excel 源正常工作。  
  
1.  在中**解决方案资源管理器**窗口中，单击**项目**菜单中，然后单击**CleanseAndCurateSuppliers 属性**。  
  
2.  在中**属性**对话框框中，展开**配置属性**左侧，然后单击**调试**。  
  
3.  设置**Run64BitRuntime**到**False**。  
  
     ![CleanseAndCurateSuppliers 项目属性](../../2014/tutorials/media/et-buildingandrunningthessisproject-01.jpg "CleanseAndCurateSuppliers 项目属性")  
  
4.  单击**确定**以关闭**属性**对话框。  
  
5.  单击**构建**菜单栏，然后单击**生成 CleanseAndCurateSuppliers**。 确保没有生成错误。  
  
6.  单击**调试**在菜单栏上单击**开始调试**。  
  
7.  查看中的消息**进度**窗口并验证是否成功执行并结束该包。  
  
     ![从进度窗口结果](../../2014/tutorials/media/et-buildingandrunningthessisproject-02.jpg "个进度窗口的结果")  
  
     ![进度窗口的最终状态](../../2014/tutorials/media/et-buildingandrunningthessisproject-03.jpg "进度窗口的最终状态")  
  
8.  单击**调试**菜单栏，然后单击**停止调试**以停止调试会话。 如果包失败，应启用数据查看器并查看数据在组件之间的流动方式。  
  
## <a name="next-step"></a>下一步  
 [任务 16:验证使用主数据管理器](../../2014/tutorials/task-16-verifying-with-master-data-manager.md)  
  
  
