---
title: "配置和管理 |Microsoft 文档"
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e0fd4554-60c6-4181-ac4c-2e366fb434f6
caps.latest.revision: "7"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 847ece72abb792d12294c83cace7b26511dafffe
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2017
---
# <a name="configuration-and-management"></a>配置和管理

这篇文章提供有关如何配置服务器以支持这些产品中的机器学习与 SQL Server 的服务的更多详细信息的链接：

+ SQL Server 2016 R Services （数据库）
+ SQL Server 自 2017 年 1 机器学习服务 （数据库）

> [!NOTE]
> 
> 此内容最初已针对 SQL Server 2016 版本中，支持仅将 R 语言编写。
> 
> 在 SQL Server 自 2017 年，对支持 Python 现已添加，但基础的体系结构和服务框架是相同的。 因此，你可以配置安全、 内存、 资源调控和其他选项来支持相同的方式的 R 脚本的执行 Python 脚本。
> 
> 但是，因为对 Python 是一种新功能、 潜在的优化有关的详细的信息，对于还没有 Python 工作负荷的支持。 请稍后再试。

## <a name="r-package-management"></a>R 包管理

这些主题描述如何在 SQL Server 实例上安装新的 R 包，管理 R 包库和数据库还原后还原包库。

+ [安装和管理 R 包](installing-and-managing-r-packages.md)
+ [安装新的 R 包](install-additional-r-packages-on-sql-server.md)
+ [为使用数据库角色实例启用包管理](r-package-how-to-enable-or-disable.md)
+ [创建本地包存储库使用 miniCRAN](create-a-local-package-repository-using-minicran.md)
+ [确定 SQl Server 上安装的 R 包](determine-which-packages-are-installed-on-sql-server.md)
+ [SQL Server 和文件系统之间的同步 R 包](package-install-uninstall-and-sync.md)
+ [安装用户库中的 R 包](packages-installed-in-user-libraries.md)

## <a name="service-configuration"></a>服务配置

这些主题描述如何对基础服务体系结构进行更改以及如何管理与扩展服务关联的安全主体。

+ [安全注意事项](security-considerations-for-the-r-runtime-in-sql-server.md)
+ [修改 SQL Server R Services 的用户帐户池](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)
+ [配置和管理高级分析扩展](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)
+ [为使用数据库角色实例启用包管理](r-package-how-to-enable-or-disable.md)
+ [性能优化 R Services](sql-server-r-services-performance-tuning.md)

## <a name="resource-governance"></a>资源调控

这些主题描述如何实现在 Enterprise Edition 中使用资源调控器功能可用的 R 或 Python 作业的资源管理。

+ [R Services 的资源调控](../../advanced-analytics/r/resource-governance-for-r-services.md)
+ [如何为 R 创建资源池](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)

另请参阅：

+ [使用自定义 SSMS 报表的监视器 R](monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="initial-setup"></a>初始安装

可以在以下主题中找到初始设置和配置相关的更多帮助：

+ [升级和安装常见问题解答](../r/upgrade-and-installation-faq-sql-server-r-services.md)
+ [安全注意事项](../r/security-considerations-for-the-r-runtime-in-sql-server.md)
+ [R Services 的已知的问题](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)

