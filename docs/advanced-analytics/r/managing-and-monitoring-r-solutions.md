---
title: "管理和监视计算机学习解决方案 |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/26/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d455f22a-190f-4a28-9088-98a843cd5db2
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 65398ab522f7a39aae08b1f438d2fa59291e4e8f
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2018
---
# <a name="managing-and-monitoring-machine-learning-solutions"></a>管理和监视计算机学习解决方案
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍在 SQL Server 计算机学习 Services 与数据库管理员需要若要开始使用 R 和 Python 解决方案相关的功能。

**适用于：** SQL Server 2016 R Services、 SQL Server 自 2017 年 1 机器学习服务

## <a name="security"></a>Security

数据库管理员必须提供数据访问，而不仅仅是对数据科学家但为各类报表开发人员、 业务分析人员和业务数据使用者。 R （与现在 Python） 到 SQL Server 的集成提供支持数据科学角色的数据库管理员提供许多好处。

+ [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的体系结构可保证数据库的安全性，并将 R 会话执行从数据库实例操作中隔离出来。

+ 你可以指定有权执行 R 脚本的人员，并确保使用在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中定义的同一安全角色来管理 R 作业中使用的数据。

+ 数据库管理员可以使用角色管理的 R 包的安装和执行的 R 和 Python 脚本。

有关详细信息，请参阅以下资源：

+ [SQL Server 中 R 运行时的安全注意事项](../../advanced-analytics/r/security-considerations-for-the-r-runtime-in-sql-server.md)

+ [R 安全概述](../r/security-overview-sql-server-r.md)

+ [Python 安全概述](../python/security-overview-sql-server-python-services.md)

+ [安装和管理 R 包](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)

## <a name="configuration-and-management"></a>配置和管理

数据库管理员必须将存在竞争的项目和优先级集成到一个联系点中，即数据库服务器。 在保持运行状况的操作和报告数据存储区时，它们必须支持分析。 机器学习与 SQL Server 的集成到数据库的管理员，越来越多地充当关键的角色中部署的数据科学高效基础结构提供许多好处。

+ 在单独的进程，以确保继续按常规方式运行，即使外部脚本运行时出现问题你的服务器中执行的 R 和 Python 的会话。

+ 低特权物理用户帐户用于包含和隔离外部脚本活动。

+ DBA 可以使用标准的 SQL Server 资源管理工具来控制分配给 R 运行时，以防止海量计算降低服务器的整体性能的资源量。

有关详细信息，请参阅以下资源：

+ [R Services 的资源调控](../r/resource-governance-for-r-services.md)

+ [配置和管理高级分析扩展](../r/configure-and-manage-advanced-analytics-extensions.md)
