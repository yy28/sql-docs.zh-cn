---
title: SQL Server 复制“发布服务器设置”对话框 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publishersettings.f1
helpviewer_keywords:
- Publisher Settings dialog box
ms.assetid: 4fb70427-082d-4179-82a1-34b235accc43
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1f1100f1c19a658fa6fe4b90816dca948e640a76
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63262308"
---
# <a name="sql-server-replication-publisher-settings-dialog-box"></a>SQL Server 复制“发布服务器设置”对话框
  可以使用 **“发布服务器设置”** 对话框，更改已添加到复制监视器左窗格中的发布服务器的设置。  
  
## <a name="options"></a>选项  
 **发布服务器连接**  
 单击此项可打开 **“连接到服务器”** 对话框，通过该对话框可以查看和更改复制监视器用来连接发布服务器的连接属性和凭据。  
  
 **分发服务器连接**  
 只有当发布服务器使用了远程分发服务器时，才会显示此项。 单击此项可打开 **“连接到服务器”** 对话框，通过该对话框可以查看和更改复制监视器用来连接远程分发服务器的连接属性和凭据。  
  
 **复制监视器启动时自动连接**  
 选择此项可以使复制监视器自动连接到分发服务器，并检索在该对话框顶部网格中所选发布服务器的状态信息。 如果清除了此复选框，则必须在启动复制监视器后手动进行连接：在复制监视器左窗格中右键单击发布服务器，然后单击 **“连接”**。  
  
 **自动刷新此发布服务器及其发布的状态**  
 选择此项可以使复制监视器自动刷新在该对话框顶部网格中所选发布服务器的状态。 如果选择了此选项，复制监视器将轮询分发服务器，以获取发布服务器及其发布的状态信息。 轮询间隔是由 **“刷新速率”** 选项设置的。 有关在复制监视器中刷新的详细信息，请参阅[缓存、刷新和复制监视器性能](monitor/caching-refresh-and-replication-monitor-performance.md)。  
  
 **“刷新速率”**  
 输入一个值（秒），指定复制监视器对分发服务器的轮询频率（以了解状态信息）。 值越小表示轮询越频繁，如果监视大量的发布服务器，则可能会影响分发服务器的性能。 建议您测试系统，以确定一个适当的值。 如果在复制监视器的任意详细信息窗口中选择 **“自动刷新”** ，则也将使用 **“刷新速率”** 设置。  
  
 **在以下组中显示此发布服务器**  
 从该列表中选择某个发布服务器组。 该发布服务器显示在左窗格中此组下面。 通过组可以组织发布服务器，而且对复制的功能没有任何影响。  
  
 **新建组**  
 单击此项可创建新的发布服务器组。 发布服务器组提供了在复制监视器内组织发布服务器的简便方法。 组既不影响数据的复制，也不影响复制拓扑中服务器之间的关系。  
  
## <a name="see-also"></a>请参阅  
 [启动复制监视器](monitor/start-the-replication-monitor.md)   
 [监视复制](monitoring-replication.md)  
  
  
