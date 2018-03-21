---
title: "故障排除和 SQL Server 中的机器学习的常见问题 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2018
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 5b9a5c6497781ef67d9d2ef9b9032a4d9ee250e5
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2018
---
# <a name="troubleshoot-machine-learning"></a>解决机器学习
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供了故障排除的链接，安装程序指南、 已知的问题和发行说明。 其他文章链接这篇文章中提供有关 SQL Server 中的计算机学习解决方案的性能优化建议。

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

+ [安装 SQL Server 自 2017 年 1 机器学习 Services （数据库）](install/sql-machine-learning-services-windows-install.md)
+ [安装 SQL Server 自 2017 年 1 机器学习服务器 （独立）](install/sql-machine-learning-standalone-windows-install.md)
+ [安装 SQL Server 2016 R Services （数据库）](install/sql-r-services-windows-install.md)
+ [安装 SQL Server 2016R Server （独立）](install/sql-r-standalone-windows-install.md)
+ [命令提示符安装程序](install/sql-ml-component-commandline-install.md)
+ [脱机安装程序 (没有 internet)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>配置

下列文章包含有关默认值的信息以及如何自定义机器学习的实例上的配置：

+ [为 SQL Server R Services 中修改用户帐户池](r/modify-the-user-account-pool-for-sql-server-r-services.md)  
+ [配置和管理高级的分析扩展](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [如何创建资源池](r/how-to-create-a-resource-pool-for-r.md)
+ [R 工作负荷的优化](r/operationalizing-your-r-code.md)
