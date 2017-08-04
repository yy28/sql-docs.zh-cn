---
title: "开始使用缩小单台计算机上的 SSIS 缩放 |Microsoft 文档"
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
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7175c63be4c0e15e50f2020f75d283ac0e3dfdbf
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="get-started-with-integration-services-ssis-scale-out-on-a-single-computer"></a>要开始使用 Integration Services (SSIS) 向外扩展单台计算机上
本部分提供的集成服务向外扩展环境中建立一台机器使用默认设置的指导。

## <a name="1-install-sql-server-features"></a>1.安装 SQL Server 功能
在 SQL Server 安装向导中，选择数据库引擎服务、 Integration Services、 缩放出 Master 和横向扩展辅助进程上**功能选择**页。

![功能选择 Onebox 1](media/feature-select-onebox1.PNG)

![功能选择 Onebox 2](media/feature-select-onebox2.PNG)

上**服务器配置**页上，只需单击"下一步"以使用默认服务帐户和启动类型。

上**数据库引擎配置**页上，选择"**混合模式**"并单击"**添加当前用户**"按钮。 

![引擎配置](media/engine-config.PNG)

一个**Integration Services 横向扩展配置的主节点**和**Integration Services 横向扩展配置的辅助节点**页，只需单击"下一步"以应用默认设置的端口和证书。

完成 SQL Server 安装向导。

## <a name="2-install-sql-server-management-studio"></a>2.安装 SQL Server Management Studio

[下载](../../ssms/download-sql-server-management-studio-ssms.md)SQL Server Management Studio 并将其安装。

## <a name="3-enable-scale-out"></a>3.启用横向扩展
打开 SSMS 并连接到本地 Sql Server 实例。
右键单击**Integration Services 目录**在对象资源管理器，选择**创建目录**。

在**创建目录**对话框中，**启用此服务器用作 SSIS 扩展 master**默认处于选中状态。 只需像往常一样创建目录。 

## <a name="4-enable-scale-out-worker"></a>4.启用横向扩展辅助进程
在 SSMS 中，右键单击**SSISDB**和选择**管理横向扩展...**. 
![管理向外扩展](media/manage-scale-out.PNG)

集成服务横向扩展管理器将弹出。 你可以使用它来管理向外扩展。 有关详细信息，请参阅[集成服务缩放出 Manager](integration-services-ssis-scale-out-manager.md)。

若要启用横向扩展辅助，请切换到**工作线程管理器**，然后选择你想要启用的辅助进程。 工作线程最初处于禁用状态。 单击**启用辅助**来启用它。

## <a name="5-run-packages-in-scale-out"></a>5.在 Scale Out 中运行包
现在，你已准备好在向外扩展运行 SSIS 包。 请参阅[Integration Services (SSIS) 中的运行的包向外扩展](run-packages-in-integration-services-ssis-scale-out.md)。


若要添加更多的向外扩展辅助进程，请参阅[添加横向扩展辅助进程与缩放出 Manager](add-scale-out-worker.md)。
