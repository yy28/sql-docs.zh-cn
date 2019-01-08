---
title: 故障排除和机器学习-SQL Server 机器学习服务的常见问题
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8cc89ee500e9240ef1fff085a34d9c1792c3e80c
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432110"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>对 SQL Server 中的机器学习进行故障排除
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

使用此页作为起点来完成的已知问题。

**适用范围：** SQL Server 2016 R Services、 SQL Server 2017 机器学习服务 （R 和 Python）

## <a name="known-issues"></a>已知问题

以下文章介绍了当前和以前版本的已知的问题：

+ [R Services 的已知的问题](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [SQL Server 2016 发行说明](../sql-server/sql-server-2016-release-notes.md)
+ [SQL Server 2017 发行说明](../sql-server/sql-server-2017-release-notes.md)

## <a name="how-to-gather-system-information"></a>如何收集系统信息

如果您已遇到错误，或需要了解你的环境中的问题，很重要系统地收集相关的信息。 以下文章获取技术支持提供信息可帮助进行故障排除，自助服务或请求的列表。

+ [数据收集的机器学习进行故障排除](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>安装和配置指南

如果未设置机器学习与 SQL Server，或如果想要添加此功能下，从此处开始：

+ [安装 SQL Server 2017 机器学习服务 （数据库内）](install/sql-machine-learning-services-windows-install.md)
+ [安装 SQL Server 2017 机器学习服务器 （独立版）](install/sql-machine-learning-standalone-windows-install.md)
+ [安装 SQL Server 2016 R Services （数据库内）](install/sql-r-services-windows-install.md)
+ [安装 SQL Server 2016 R Server （独立版）](install/sql-r-standalone-windows-install.md)
+ [命令提示符下安装程序](install/sql-ml-component-commandline-install.md)
+ [脱机设置（无 Internet）](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>配置

以下文章包含有关默认值的信息以及如何自定义机器学习的实例上的配置：

+ [缩放并发执行的 SQL Server 机器学习服务中的外部脚本的](administration/modify-user-account-pool.md)   
+ [配置和管理高级的分析扩展](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [如何创建资源池](r/how-to-create-a-resource-pool-for-r.md)
+ [适用于 R 工作负荷的优化](r/operationalizing-your-r-code.md)
