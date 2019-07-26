---
title: 机器学习的故障排除和常见问题
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 86c698420a64832e49cd6cbff5e6727896ec45f4
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470272"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>SQL Server 中的机器学习疑难解答
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

使用此页作为了解已知问题的起点。

**适用范围：** SQL Server 2016 R Services SQL Server 2017 机器学习服务 (R 和 Python)

## <a name="known-issues"></a>已知问题

以下文章介绍了当前版本和以前版本的已知问题:

+ [R Services 的已知问题](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [SQL Server 2016 发行说明](../sql-server/sql-server-2016-release-notes.md)
+ [SQL Server 2017 发行说明](../sql-server/sql-server-2017-release-notes.md)

## <a name="how-to-gather-system-information"></a>如何收集系统信息

如果遇到错误, 或需要了解环境中的问题, 请务必系统地收集相关信息。 以下文章提供了有助于自助故障排除或请求技术支持的信息列表。

+ [机器学习故障排除的数据收集](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>安装和配置指南

如果尚未使用 SQL Server 设置机器学习, 或者要添加此功能, 请从此处开始:

+ [安装 SQL Server 2017 机器学习服务 (数据库内)](install/sql-machine-learning-services-windows-install.md)
+ [安装 SQL Server 2017 Machine Learning Server (独立版)](install/sql-machine-learning-standalone-windows-install.md)
+ [安装 SQL Server 2016 R Services （数据库内）](install/sql-r-services-windows-install.md)
+ [安装 SQL Server 2016 R Server (独立版)](install/sql-r-standalone-windows-install.md)
+ [命令提示符设置](install/sql-ml-component-commandline-install.md)
+ [脱机设置（无 Internet）](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>配置

以下文章包含有关默认设置的信息, 以及如何在实例上自定义机器学习的配置:

+ [在 SQL Server 机器学习服务中扩展外部脚本的并发执行](administration/modify-user-account-pool.md)   
+ [配置和管理高级分析扩展](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [如何创建资源池](r/how-to-create-a-resource-pool-for-r.md)
+ [R 负载优化](r/operationalizing-your-r-code.md)
