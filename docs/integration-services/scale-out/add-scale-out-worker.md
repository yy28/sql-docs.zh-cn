---
title: "使用 Scale Out Manager 添加 SSIS Scale Out Worker | Microsoft Docs"
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
ms.openlocfilehash: ef11448d03bd188aaea425225312af9f681f530c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="add-a-scale-out-worker-with-scale-out-manager"></a>使用 Scale Out Manager 添加 Scale Out Worker

Integration Services Scale Out Manager 极大地降低了将 Scale Out Worker 添加到现有 Scale Out 环境的复杂性。 

可按照以下步骤将 Scale Out Worker 添加到 Scale Out 拓扑：

## <a name="1-install-scale-out-worker"></a>1.安装 Scale Out Worker
在 SQL Server 安装向导中，在“功能选择”页上选择 Integration Services 和 Scale Out Worker。 
![功能选择 Worker](media/feature-select-worker.PNG)

在“Integration Services Scale Out 配置 - 辅助角色节点”页上，只需单击“下一步”即可跳过此处的配置，并使用“Scale Out Manager”完成安装后的配置。

完成安装向导。

## <a name="2-open-firewall-on-scale-out-master-computer"></a>2.打开 Scale Out Master 计算机上的防火墙
使用 Scale Out Master 计算机上的 Windows 防火墙，打开在 Scale Out Master 安装期间指定的端口（默认为 8391）和 SQL Server 端口（默认为 1433）。

## <a name="3-add-scale-out-worker-with-scale-out-manager"></a>3.使用 Scale Out Manager 添加 Scale Out Worker
以管理员身份运行 SQL Server Management Studio 并连接到 Scale Out Master 的 SQL Server 实例。

右键单击对象资源管理器中的“SSISDB”，并选择“管理 Scale Out...”。 

![管理 Scale Out](media/manage-scale-out.PNG)

在弹出的“Scale Out Manager”中，切换到“Worker 管理器”。 单击“+”按钮，并按照“连接 Worker”对话框中的说明进行操作。 有关详细信息，请参阅 [Scale Out Manager](integration-services-ssis-scale-out-manager.md)。
