---
title: 任务15：生成并运行 SSIS 项目 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66822995"
---
# <a name="task-15-building-and-running-the-ssis-project"></a>任务 15：生成和运行 SSIS 项目

  在本任务中，您将生成并运行 SSIS 项目。 如果在计算机上安装了64位版本的 Excel 2010，则应将**Run64BitRuntime**的值设置为**False** ，以便 Excel 源工作。  
  
1.  在 "**解决方案资源管理器**" 窗口中，单击菜单上的 "**项目**"，然后单击 " **CleanseAndCurateSuppliers 属性**"。  
  
2.  在 "**属性**" 对话框中，展开左侧的 "**配置属性**"，然后单击 "**调试**"。  
  
3.  将**Run64BitRuntime**设置为**False**。  
  
     ![CleanseAndCurateSuppliers 项目属性](../../2014/tutorials/media/et-buildingandrunningthessisproject-01.jpg "CleanseAndCurateSuppliers 项目属性")  
  
4.  单击 **"确定"** 以关闭 "**属性**" 对话框。  
  
5.  单击菜单栏上的 "**生成**"，然后单击 "**生成 CleanseAndCurateSuppliers**"。 确保没有生成错误。  
  
6.  单击菜单栏上的 "**调试**"，然后单击 "**启动调试**"。  
  
7.  查看 "**进度**" 窗口中的消息，并验证包是否已成功执行和结束。  
  
     ![进度窗口的结果](../../2014/tutorials/media/et-buildingandrunningthessisproject-02.jpg "进度窗口的结果")  
  
     ![进度窗口的最终状态](../../2014/tutorials/media/et-buildingandrunningthessisproject-03.jpg "进度窗口的最终状态")  
  
8.  单击菜单栏上的 "**调试**"，然后单击 "**停止调试**" 以停止调试会话。 如果包失败，应启用数据查看器并查看数据在组件之间的流动方式。  
  
## <a name="next-step"></a>下一步  
 [任务 16：使用主数据管理器进行验证](../../2014/tutorials/task-16-verifying-with-master-data-manager.md)  
  
  
