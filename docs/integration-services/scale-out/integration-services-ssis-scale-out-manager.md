---
title: SQL Server Integration Services Scale Out Manager | Microsoft Docs
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 84fe58d4dc7894728c43cb19d17d3444b5b84820
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="integration-services-scale-out-manager"></a>Integration Services Scale Out Manager

Scale Out Manager 是一种管理工具，可用于在单一位置管理完整的 SSIS Scale Out 拓扑。 它消除了多台计算机上运行和处理 TSQL 命令的负担。 

可通过两种方式触发 Scale Out Manager。

## <a name="1-open-scale-out-manager-from-sql-server-management-studio"></a>1.从 SQL Server Management Studio 打开 Scale Out Manager
打开 SQL Server Management Studio 并连接到 Scale Out Master 的 SQL Server 实例。

右键单击对象资源管理器中的“SSISDB”，并选择“管理 Scale Out...”。![管理 Scale Out](media/manage-scale-out.PNG)

> [!NOTE]
> 建议以管理员身份运行 SQL Server Management Studio，因为一些 Scale Out 管理操作（如“添加 Scale Out Worker”）需要管理权限。


## <a name="2-open-scale-out-manager-by-runing-ismanagerexe-directly"></a>2.通过直接运行 ISManager.exe 打开 Scale Out Manager

ISManager.exe 位于 %SystemDrive%\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn\Management 下。 右键单击“ISManager.exe”并选择“以管理员身份运行”。 

打开后，需要先输入 Scale Out Master 的 SQL Server 名称并与其建立连接，才可管理 Scale Out。

![门户连接](media/portal-connect.PNG)

Scale Out Manager 提供多种功能，如下所示。 

## <a name="enable-scale-out"></a>启用 Scale Out
连接到 SQL Server 后，如果未启用 Scale Out，可以单击"启用"按钮启用它。

![在门户中启用 Scale Out](media/portal-enable-scale-out.PNG) 
## <a name="view-scale-out-master-status"></a>查看 Scale Out Master 状态
Scale Out Master 的状态显示在“仪表板”页上。

![门户仪表板](media/portal-dashboard.PNG)
## <a name="view-scale-out-worker-status"></a>查看 Scale Out Worker 状态
Scale Out Master 的状态显示在“Worker 管理器”页上。 可单击每个辅助角色来查看单个状态。

![门户中的 Worker 管理器](media/portal-worker-manager.PNG)

## <a name="add-scale-out-worker"></a>添加 Scale Out Worker
要添加 Scale Out Worker，请单击 Scale Out Worker 列表底部的“+”按钮。 

输入想要添加的 Scale Out Worker 的计算机名称，然后单击“验证”。 Scale Out Worker 会检查当前用户是否有权访问 Scale Out Master 和 Scale Out Worker 计算机上的证书存储。

![连接 Worker](media/connect-worker.PNG)

如果验证通过，Scale Out Manager 会尝试读取辅助角色配置文件并获取辅助角色的证书指纹。 有关详细信息，请参阅[Scale Out Worker](integration-services-ssis-scale-out-worker.md)。 如果无法读取辅助角色配置文件，可通过两种替代方式提供辅助角色证书。 

可直接输入辅助角色证书的指纹 

![辅助角色证书 1](media/portal-cert1.PNG)

也可提供证书文件。 

![辅助角色证书 2](media/portal-cert2.PNG)

收集所有信息后，“Scale Out Manager”可提供要执行的操作。 通常包括证书安装、辅助角色配置文件更新和辅助角色服务重启。 

![门户中的添加确认 1](media/portal-add-confirm1.PNG)

如果无法访问辅助角色证书，需要自行手动更新并重启辅助角色服务。

![门户中的添加确认 2](media/portal-add-confirm2.PNG)

单击“确认”复选框并开始添加 Scale Out Worker。

## <a name="delete-scale-out-worker"></a>删除 Scale Out Worker
要删除 Scale Out Worker，请选择 Scale Out Worker 并单击 Scale Out Worker 列表底部的“-”按钮。


## <a name="enabledisable-scale-out"></a>启用/禁用 Scale Out
要启用或禁用 Scale Out Worker，请选择 Scale Out Worker 并单击“启用 Worker”或“禁用 Worker”按钮。 如果辅助角色处于联机状态，Scale Out Manager 上的辅助角色状态会发生相应的更改。

## <a name="edit-scale-out-worker-description"></a>编辑 Scale Out Worker 描述
要编辑 Scale Out Worker 的描述，选择 Scale Out Worker 并单击“编辑”按钮。 完成编辑后，单击“保存”按钮。

![在门户中保存 Worker](media/portal-save-worker.PNG)

