---
title: 查看资源运行状况策略结果（SQL Server 实用工具）| Microsoft Docs
description: 了解如何使用 SQL Server Management Studio 查看 SQL Server 和数据层应用程序实例的 SQL Server 实用工具资源运行状况策略结果。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 80cb14fb-f4c6-4be2-ba17-eb4e4cddd35f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a3ec26ba8988f36e3deac88373a932ef377f8d59
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810020"
---
# <a name="view-resource-health-policy-results-sql-server-utility"></a>查看资源运行状况策略结果（SQL Server 实用工具）

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的实用工具仪表板，可以查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例和数据层应用程序的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具资源参数。 有关详细信息，请参阅 [SQL Server 实用工具功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  

##  <a name="SSMSProcedure"></a>

### <a name="view-sql-server-utility-resource-health-policy-results"></a>查看 SQL Server 实用工具的资源运行状况策略结果  

1. 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) 中，选择“视图”，然后选择“实用工具资源管理器”，查看“实用工具资源管理器”导航窗格 。 若要查看内容窗格，请选择“视图”，然后选择“实用工具资源管理器内容” 。  

2. 在导航窗格中，选择 ![连接到实用工具](../../relational-databases/manage/media/connect-to-utility.gif "Connect_to_Utility")“连接到实用工具”。 如果尚未创建实用工具控制点 (UCP)，或者尚未将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例或者数据层应用程序注册到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中，请参阅 [SQL Server 实用工具功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  

3. 选择 UCP 节点可查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例和数据层应用程序的摘要数据（右键单击可刷新）。 面板数据将显示在内容窗格中。  

4. 选择“托管实例”节点可查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例的列表视图数据（右键单击可刷新）。 列表视图数据将显示在内容窗格中。  

5. 选择“已部署的数据层应用程序”节点可查看数据层应用程序的列表视图（右键单击可刷新）。 列表视图数据将显示在内容窗格中。  

## <a name="see-also"></a>另请参阅

- [SQL Server 实用工具功能和任务](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)
- [减少 CPU 使用策略中的干扰（SQL Server 实用工具）](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)
- [已部署的数据层应用程序详细信息（SQL Server 实用工具）](/previous-versions/sql/sql-server-2016/ee240857(v=sql.130))
- [托管实例详细信息（SQL Server 实用工具）](./utility-explorer-f1-help.md)
- [实用工具管理（SQL Server 实用工具）](/previous-versions/sql/sql-server-2016/ee240832(v=sql.130))