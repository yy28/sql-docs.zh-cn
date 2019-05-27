---
title: 添加数据流性能计数器的日志 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- performance counters [Integration Services]
- counters [Integration Services]
- logs [Integration Services], data flow counters
ms.assetid: b500d166-33ba-4b82-a92d-b0a333924e8d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 76c85de1e9e8c294ab9db1f887f2b417b321d663
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66062061"
---
# <a name="add-a-log-for-data-flow-performance-counters"></a>添加数据流性能计数器的日志
  本过程介绍如何为数据流引擎提供的性能计数器添加日志。  
  
> [!NOTE]  
>  如果在运行 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的计算机上安装 [!INCLUDE[winxpsvr](../includes/winxpsvr-md.md)]，然后将该计算机升级到 [!INCLUDE[firstref_longhorn](../includes/firstref-longhorn-md.md)]，则升级过程会从该计算机删除 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 性能计数器。 若要还原计算机上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 性能计数器，请在修复模式下运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安装程序。  
  
### <a name="to-add-logging-of-performance-counters"></a>添加性能计数器的日志记录  
  
1.  在 **“控制面板”** 中，如果您使用的是经典视图，请单击 **“管理工具”**。 如果使用的是分类视图，请单击 **“性能和维护”** ，再单击 **“管理工具”**。  
  
2.  单击 **“性能”**。  
  
3.  在“性能”对话框中，展开“性能日志和警报”，右键单击“计数器日志”，再单击“新建日志设置”。 键入日志的名称。 例如，键入 **MyLog**。  
  
4.  单击“确定” 。  
  
5.  在 **MyLog** 对话框中，单击 **“添加计数器”**。  
  
6.  单击 **“使用本地计算机计数器”** 记录本地计算机上性能计数器的日志，或者单击 **“从计算机选择计数器”** ，然后从列表中选择计算机，以记录该指定的计算机的性能计数器的日志。  
  
7.  在 **“添加计数器”** 对话框中，选择 **“性能对象”** 列表中的 **“SQL Server:SSIS 管道”** 。  
  
8.  若要选择性能计数器，请执行下列操作之一：  
  
    -   选择 **“所有计数器”** 以记录所有性能计数器的日志。  
  
    -   选择 **“选择列表中的计数器”** ，然后选择要使用的性能计数器。  
  
9. 单击 **“添加”**。  
  
10. 单击 **“关闭”**。  
  
11. 在 **MyLog** 对话框中，检查 **“计数器”** 列表中记录日志的性能计数器的列表。  
  
12. 若要添加其他计数器，请重复步骤 5 到步骤 10。  
  
13. 单击“确定” 。  
  
    > [!NOTE]  
    >  必须使用属于 Administrators 组成员的本地帐户或域帐户启动性能日志和警报服务。  
  
## <a name="see-also"></a>请参阅  
 [性能计数器](performance/performance-counters.md)   
 [在“日志事件”窗口中查看日志项](../../2014/integration-services/view-log-entries-in-the-log-events-window.md)  
  
  
