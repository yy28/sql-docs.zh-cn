---
title: 故障排除和 SQL Server 中的机器学习的常见问题 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6ef72ae56973e695b96f0dfac7c0a3414bca5225
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34707355"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>解决 SQL Server 中的机器学习
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

使用此页作为起始点来完成已知问题。

**适用于：** SQL Server 2016 R Services、 SQL Server 自 2017 年 1 机器学习服务 （R 和 Python）

## <a name="known-issues"></a>已知问题

以下文章介绍当前和以前版本的已知的问题：

+ [R Services 的已知的问题](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [SQL Server 2016 发行说明](../sql-server/sql-server-2016-release-notes.md)
+ [SQL Server 2017 发行说明](../sql-server/sql-server-2017-release-notes.md)

## <a name="how-to-gather-system-information"></a>如何收集系统信息

如果你已遇到错误，或需要了解你的环境中的问题，则很重要系统地收集相关的信息。 以下文章提供有关技术支持的信息，它方便了自助诊断或请求列表。

+ [用于机器学习故障排除数据收集](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>安装和配置指南

如果不设置机器学习与 SQL Server，或如果你想要添加功能下，从此处开始：

+ [安装 SQL Server 自 2017 年 1 机器学习 Services （数据库）](install/sql-machine-learning-services-windows-install.md)
+ [安装 SQL Server 自 2017 年 1 机器学习服务器 （独立）](install/sql-machine-learning-standalone-windows-install.md)
+ [安装 SQL Server 2016 R Services （数据库）](install/sql-r-services-windows-install.md)
+ [安装 SQL Server 2016 R Server （独立）](install/sql-r-standalone-windows-install.md)
+ [命令提示符安装程序](install/sql-ml-component-commandline-install.md)
+ [脱机设置（无 Internet）](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>配置

下列文章包含有关默认值的信息以及如何自定义机器学习的实例上的配置：

+ [为 SQL Server R Services 中修改用户帐户池](r/modify-the-user-account-pool-for-sql-server-r-services.md)  
+ [配置和管理高级的分析扩展](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [如何创建资源池](r/how-to-create-a-resource-pool-for-r.md)
+ [R 工作负荷的优化](r/operationalizing-your-r-code.md)
