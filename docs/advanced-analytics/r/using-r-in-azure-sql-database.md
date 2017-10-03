---
title: "使用 Azure SQL 数据库中的 R |Microsoft 文档"
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 1
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e3c781449a8f7a1b236508cd21b8c00ff175774f
ms.openlocfilehash: 619921bbf00801fd5930a1c1b110e69a9fd05a81
ms.contentlocale: zh-cn
ms.lasthandoff: 09/30/2017

---
# <a name="using-r-in-azure-sql-database"></a>在 Azure SQL Database 中使用 R

截至自 2017 年 10 月，Azure SQL Database 支持的 R 代码数据库中使用类似于 SQL Server 2016 中的 R Services 的存储的过程的执行。

这篇文章提供功能的概述，并描述了已知的限制。

> [!NOTE]
> 此版本是初始预览版本，适用于测试和仅浏览。 将一段时间在 2018年中发布的生产版本。 确切的发布日期和生成，将根据用户反馈。 因此我们建议你尝试使用该功能，并让我们知道哪些功能很重要。 
> 
> 有关发布计划的信息，请参阅[SQL Server 博客](https://blogs.technet.microsoft.com/dataplatforminsider/)或[Microsoft R Server 博客](https://blogs.msdn.microsoft.com/rserver/)。

## <a name="features"></a>功能

预览版本提供以下功能：

+ 调用 R 使用存储过程以便于部署的计算机学习解决方案
+ 从模型使用的任何应用程序可以连接到你的云数据库中获取评分
+ 支持使用预测函数中，以快速获得评分，无需使用 R 运行时本机评分

有关限制特定于预览版本，请参阅[限制和已知的问题](#bkmk_restrictions)。

### <a name="components"></a>Components

总体体系结构是类似的 SQL Server 机 R Services。

**安全性**

+ SQL Server 受信任的启动板管理 R 作业的执行，并控制进程的生存期。 

**R 包**

+ 预览版本包含 Microsoft R Open 3.3.3 和 Microsoft R Server 9.2 版。 [RevoScaleR 包](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)已预装。

+ 已删除或修改降低在 Azure 环境中的空间占用量某些 R 包。 例如， **mrsdeploy**不包括在 Azure SQL 数据库。

**“性能”**

+ 定型集和评分从任何模型数据适合在内存中的支持。  可用内存量取决于数据库的版本。 
+ 使用支持普通的并行@parallel= 1 个参数，以及用于执行 R 脚本的流式处理 
+ 在预览版中，限制为每个数据库的并发执行的单个 R 脚本。

**语言**

未来版本的路线图包括支持其他包和 Python。

## <a name="restrictions"></a>限制

本部分列出了一些其他限制适用于预览版本。

### <a name="upgrading-r-components-and-adding-packages-not-supported"></a>升级 R 组件和添加不受支持的程序包

Azure SQL 数据库是一个托管的服务，并不应客户管理的 R 组件升级。 对于预览版本，请使用可用的安装的包。

随着变得可用，则将发布到 R 和其他机器学习组件的升级。

### <a name="availability"></a>可用性

运行 R 和其他机器学习 Azure SQL 数据库中的脚本的能力是一项预览功能仅中央美国西部区域中。 扩展到其他区域，例如西欧，计划于更高版本。

在 Azure SQL 数据库中运行 R 需要足够存储和内存。 当前支持以下数据库服务层和性能级别：

+ 高级服务层： P1、 P2、 P4、 P6、 P11、 P15 
+ 高级 RS 服务层： PRS1，PRS2，PRS4 PRS6 
+ 高级弹性池： 125 弹性 Dtu 或更高版本 
+ 高级 RS 弹性池： 125 Edtu 或更高版本 

### <a name="resource-management"></a>资源管理

此版本不支持具有自定义 R 安装中，或要监视的 R 脚本使用的能力。

例如，你不能启用仅在特定的数据库上执行 R 脚本。

DMV sys.dm_db_resource_stats，用于监视 CPU 和内存使用情况的 R 脚本，在中不可用的预览版本。

### <a name="other-limitations"></a>其他限制

不支持以下功能： 

+ MicrosoftML 包不可用。
+ 不支持如创建外部库程序包管理功能。
+ 从 R 客户端执行脚本时，不能用作远程计算上下文的 Azure SQL 数据库。 必须通过使用存储的过程 sp_execute_external_script 运行 R 脚本。 调用存储过程的脚本不能使用其他计算上下文。
+ 无法执行对需要并行执行的 rx 函数的调用。
+ 不支持从 R 脚本的环回连接到 SQL Server。 换而言之，你无法进行外部调用 R 脚本从另一个 ODBC 数据源。

## <a name="get-started"></a>要开始

SQL Server 开发团队的此公告包括你可以运行在您自己的 Azure SQL 数据库进行实验，以生成 R 模型并生成预测的简短示例。

+ [训练和 Azure SQL Database 中的评分模型](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/09/25/announcing-preview-of-machine-learning-services-with-r-support-in-azure-sql-database/)

