---
title: "SQL Server Integration Services 横向扩展管理器 |Microsoft 文档"
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
ms.openlocfilehash: 96748296acd1b2f5ba98558335fece9637eadb87
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-scale-out-manager"></a>集成服务横向扩展管理器

扩展出管理器是一种管理工具，可用于管理你完整 SSIS 的横向扩展的拓扑中的单个位置。 它可让你免于多台计算机上运行，并且使用 TSQL 命令处理。 

有两种方法来触发扩展出管理器。

## <a name="1-open-scale-out-manager-from-sql-server-management-studio"></a>1.从 SQL Server Management Studio 打开横向扩展管理器
打开 SQL Server Management Studio 并连接到缩放出母版的 SQL Server 实例。

右键单击**SSISDB**在对象资源管理器，选择**管理横向扩展...**. 
![管理向外扩展](media/manage-scale-out.PNG)

> [!NOTE]
> 建议以作为一些例如"添加横向扩展辅助进程"的向外扩展管理操作的管理员身份运行 SQL Server Management Studio 将需要管理权限。


## <a name="2-open-scale-out-manager-by-runing-ismanagerexe-directly"></a>2.直接通过运行 ISManager.exe 打开横向扩展管理器

ISManager.exe %SystemDrive%\Program 文件 (x86) \Microsoft SQL Server\140\DTS\Binn\Management 下查找。 右键单击**ISManager.exe** ，然后选择"以管理员身份运行"。 

打开后，你需要输入缩放出母版的 Sql Server 名称和管理你向外扩展之前，连接到它。

![门户连接](media/portal-connect.PNG)

扩展出管理器提供各种功能，如下所示。 

## <a name="enable-scale-out"></a>启用横向扩展
连接到 SQL Server 后，如果未启用横向扩展，可以单击"启用"按钮以启用它。

![门户启用扩展](media/portal-enable-scale-out.PNG) 
## <a name="view-scale-out-master-status"></a>查看缩放出 Master 状态
在显示的状态。 缩放出 Master**仪表板**页。

![门户仪表板](media/portal-dashboard.PNG)
## <a name="view-scale-out-worker-status"></a>查看横向扩展辅助状态
在显示的状态。 横向扩展辅助**工作线程管理器**页。 你可以单击每个辅助角色，若要查看的单个状态。

![门户工作线程管理器](media/portal-worker-manager.PNG)

## <a name="add-scale-out-worker"></a>添加横向扩展辅助进程
若要添加横向扩展辅助进程，请单击横向扩展辅助列表底部的"+"按钮。 

输入你想要添加，然后单击"验证"出辅助缩放的计算机名称。 扩展出管理器将检查当前用户是否能够访问到的小数位数出 Master 和横向扩展辅助计算机上的证书存储。

![连接辅助](media/connect-worker.PNG)

如果通过验证，扩展出管理器将尝试读取配置文件的你的工作并获取证书指纹的辅助进程。 有关详细信息，请参阅[横向扩展辅助](integration-services-ssis-scale-out-worker.md)。 如果不能读取配置文件的工作线程，有两种替代方式来提供的辅助证书。 

你可以直接输入辅助证书的指纹 

![工作线程证书 1](media/portal-cert1.PNG)

或提供的证书文件。 

![工作线程证书 2](media/portal-cert2.PNG)

收集所有信息后，扩展出管理器将提供要执行的操作。 Tyically，它包括证书安装、 辅助角色配置文件更新和辅助服务重新启动。 

![门户添加确认 1](media/portal-add-confirm1.PNG)

如果工作线程证书不可访问，你需要手动自行对其进行更新并重新启动辅助服务。

![门户添加确认 2](media/portal-add-confirm2.PNG)

单击确认复选框，并开始添加横向扩展辅助进程。

## <a name="delete-scale-out-worker"></a>删除横向扩展辅助进程
若要删除横向扩展辅助进程，请选择横向扩展辅助，然后单击"-"横向扩展辅助列表底部的按钮。


## <a name="enabledisable-scale-out"></a>启用/禁用向外扩展
若要启用或禁用横向扩展辅助进程，请选择横向扩展辅助，然后单击"启用辅助"禁用辅助"按钮。 如果该工作人员未脱机，扩展出管理器上的辅助进程状态将相应地更改。

## <a name="edit-scale-out-worker-description"></a>编辑横向扩展辅助描述
若要编辑的横向扩展辅助进程的说明，请选择横向扩展辅助，然后单击"编辑"按钮。 在完成编辑后，单击"保存"按钮。

![保存工作人员的门户](media/portal-save-worker.PNG)


