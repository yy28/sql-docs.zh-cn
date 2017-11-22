---
title: "故障排除和 SQL Server 中的机器学习的常见问题 |Microsoft 文档"
ms.custom: 
ms.date: 06/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e110a2578d6663c2c7c4c2e0dd92957744b44f4a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="troubleshoot-machine-learning"></a>解决机器学习

本文提供了与 SQL Server 中的机器学习功能的设置和配置相关的疑难解答信息。 这些信息包括设置指南、 已知的问题和发行说明的链接。 其他文章链接这篇文章中提供有关 SQL Server 中的计算机学习解决方案的性能优化建议。

使用此页作为起始点，用于查找已知的问题，安装程序的常见问题和过程进行故障排除。

**适用于：** SQL Server 2016 R Services、 SQL Server 自 2017 年 1 机器学习服务 （R 和 Python）

## <a name="known-issues"></a>已知问题

以下文章列表的当前版本中，已知的问题，或描述与早期版本的问题：

+ [R Services 的已知的问题](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [SQL Server 2016 发行说明](../sql-server/sql-server-2016-release-notes.md)
+ [SQL Server 2017 发行说明](../sql-server/sql-server-2017-release-notes.md)

## <a name="troubleshooting-prerequisites"></a>故障排除的系统必备组件

如果你已遇到错误，或需要了解你的环境中的问题，则很重要系统地收集相关的信息。 此信息包括版本、 版本、 安全上下文和执行上下文。

以下文章提供有关技术支持的信息，它方便了自助诊断或请求列表。

+ [用于机器学习故障排除数据收集](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>安装和配置指南

如果不设置机器学习与 SQL Server，或如果你想要添加功能下，从此处开始：

+ [将 R Services 或使用 R 的机器学习服务设置](../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)
+ [设置与 Python 的机器学习服务](../advanced-analytics/python/setup-python-machine-learning-services.md)
+ [安装程序常见问题](../advanced-analytics/r/upgrade-and-installation-faq-sql-server-r-services.md)
+ [使用 SqlBindR 升级 R services 的实例](../advanced-analytics/r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

以下文章介绍 SQL Server 中的机器学习功能的脱机安装程序所需的其他步骤：

+ [R Services 的无人参与的安装](../advanced-analytics/r/unattended-installs-of-sql-server-r-services.md) 
+ [具有 Python 的机器学习服务的无人参与的安装](../advanced-analytics/python/unattended-installs-of-sql-server-python-services.md)

如果你需要安装机器学习功能在无 Internet 连接的计算机上，使用本文中的链接以运行安装程序之前下载的 R 和 Python 组件：

+ [在没有连接到 Internet 的情况下安装机器学习组件](../advanced-analytics/r/installing-ml-components-without-internet-access.md)

### <a name="configuration"></a>配置

下列文章包含有关默认值的信息以及如何自定义机器学习的实例上的配置：

+ [为 SQL Server R Services 中修改用户帐户池](../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)  
+ [配置和管理高级的分析扩展](../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)  
+ [如何创建资源池](r/how-to-create-a-resource-pool-for-r.md)
+ [R 工作负荷的优化](r/operationalizing-your-r-code.md)

## <a name="related-tools-and-services"></a>相关的工具和服务

+ [设置 Microsoft 机器学习服务器独立](../advanced-analytics/r/create-a-standalone-r-server.md)
+ [设置 Azure VM 上的 R 服务器](../advanced-analytics/r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)
+ [安装 R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)
+ [获取 R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/)
