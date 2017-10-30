---
title: "添加 SSIS 向外的扩展辅助进程，在横向扩展管理器 |Microsoft 文档"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b769236330941a107865a0b133961bce5bf6b85b
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="add-a-scale-out-worker-with-scale-out-manager"></a>添加横向扩展辅助进程，在横向扩展管理器

集成服务缩放出 Manager 极大地缓解将横向扩展辅助角色添加到现有的向外扩展环境的复杂性。 

以下步骤允许您将横向扩展辅助进程添加到向外扩展拓扑：

## <a name="1-install-scale-out-worker"></a>1.安装横向扩展辅助进程
在 SQL Server 安装向导中，选择 Integration Services 和横向扩展辅助上**功能选择**页。 
![功能选择 Worker](media/feature-select-worker.PNG)

上**Integration Services 横向扩展配置的辅助节点**页上，可以只需单击"下一步"以跳过此处配置并使用**缩放出 Manager**执行安装后的配置。

完成安装向导。

## <a name="2-open-firewall-on-scale-out-master-computer"></a>2.缩放出主计算机上打开防火墙
打开在缩放出主安装 (默认情况下，8391) 和端口的 SQL Server (1433，默认情况下)，过程中指定的端口在缩放出主计算机上使用 Windows 防火墙。

## <a name="3-add-scale-out-worker-with-scale-out-manager"></a>3.添加横向扩展辅助进程，在横向扩展管理器
以管理员身份运行 SQL Server Management Studio 并连接到缩放出母版的 SQL Server 实例。

右键单击**SSISDB**在对象资源管理器，选择**管理横向扩展...**. 

![管理向外扩展](media/manage-scale-out.PNG)

在弹出向上**缩放出 Manager**，切换到**工作线程管理器**。 单击"+"按钮，然后按照连接辅助对话框上的说明。 有关详细信息，请参阅[缩放出 Manager](integration-services-ssis-scale-out-manager.md)。

