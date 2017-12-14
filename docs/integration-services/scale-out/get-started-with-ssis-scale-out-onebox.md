---
title: "在单台计算机上开始使用 SSIS Scale Out | Microsoft Docs"
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
ms.openlocfilehash: 8514cd548b003a39bf198b83b6b80d775a55384b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="get-started-with-integration-services-ssis-scale-out-on-a-single-computer"></a>在单台计算机上开始使用 Integration Services (SSIS) Scale Out
本部分指导如何在单一计算机环境中使用默认设置来设置 Integration Services Scale Out。

## <a name="1-install-sql-server-features"></a>1.安装 SQL Server 功能
在 SQL Server 安装向导的“功能选择”页上，选择数据库引擎服务、Integration Services、Scale Out Master 和 Scale Out Worker。

![功能选择 Onebox 1](media/feature-select-onebox1.PNG)

![功能选择 Onebox 2](media/feature-select-onebox2.PNG)

在“服务器配置”页上，只需单击“下一步”，以使用默认服务帐户和启动类型。

在“数据库引擎配置”页上，选择“混合模式”并单击“添加当前用户”按钮。 

![引擎配置](media/engine-config.PNG)

在“Integration Services Scale Out 配置 - 主节点”和“Integration Services Scale Out 配置 - 辅助节点”页上，只需单击“下一步”应用端口和证书的默认设置。

完成 SQL Server 安装向导。

## <a name="2-install-sql-server-management-studio"></a>2.安装 SQL Server Management Studio

[下载](../../ssms/download-sql-server-management-studio-ssms.md)并安装 SQL Server Management Studio。

## <a name="3-enable-scale-out"></a>3.启用 Scale Out
打开 SSMS 并连接到本地 SQL Server 实例。
在对象资源管理器中右键单击“Integration Services 目录”，选择“创建目录”。

在“创建目录”对话框中，“启用此服务器作为 SSIS Scale Out 主节点”默认处于选中状态。 只需像往常一样创建目录。 

## <a name="4-enable-scale-out-worker"></a>4.启用 Scale Out Worker
在 SSMS 中，右键单击“SSISDB”并选择“管理 Scale Out...”。![管理 Scale Out](media/manage-scale-out.PNG)

随即弹出 Integration Services Scale Out Manager。 可以用它来管理 Scale Out。 有关详细信息，请参阅 [Integration Services Scale Out Manager](integration-services-ssis-scale-out-manager.md)。

若要启用 Scale Out Worker，请切换到“Worker 管理器”，选择要启用的 Worker。 Worker 最初处于禁用状态。 单击“启用 Worker”启用它。

## <a name="5-run-packages-in-scale-out"></a>5.在 Scale Out 中运行包
现在可以在 Scale Out 中运行 SSIS 包。请参阅[在 Integration Services (SSIS) Scale Out 中运行包](run-packages-in-integration-services-ssis-scale-out.md)。


若要添加更多 Scale Out Worker，请参阅[使用 Scale Out Manager 添加 Scale Out Worker](add-scale-out-worker.md)。
