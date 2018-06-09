---
title: SQL Server 机器学习开发人员的嵌入的 R 分析教程 |Microsoft 文档
description: 本教程演示如何将 R 嵌入在 SQL Server 中存储过程和 T-SQL 函数
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/07/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3d2b77d73bb1b8f5d4c507b884d0a09f4647012b
ms.sourcegitcommit: b52b5d972b1a180e575dccfc4abce49af1a6b230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "35250020"
---
# <a name="tutorial-embedded-r-in-stored-procedures-and-t-sql-functions"></a>教程： 将 R 嵌入在存储的过程和 T-SQL 函数
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本教程的目标是 SQL 程序员提供生成机器学习在 SQL Server 中的解决方案的实践经验。 在本教程中，你将学习如何通过 R 代码包装在存储过程中将 R 合并到应用程序或 BI 解决方案。

> [!NOTE]
> 
> 相同的解决方案是在 Python 中可用。 SQL Server 2017 是必需的。 请参阅[数据库中分析面向 Python 开发人员](../tutorials/sqldev-in-database-python-for-sql-developers.md)

## <a name="overview"></a>概述

构建端到端解决方案的过程通常包括获取并清洗数据、数据探索和功能研发、模型训练和调优，以及最后在生产中部署模型。 开发和测试的实际代码的最佳执行使用专用的开发环境。 ，这可能意味着 RStudio 或[!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]。

但是，在创建该解决方案后，可以在熟悉的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 环境中使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程将其轻松部署到 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。

在本教程中，我们假定您已被授予的解决方案和专注于构建和部署使用 SQL Server 的解决方案所需的所有 R 代码。

- [第 1 课： 下载的示例数据和脚本](../tutorials/sqldev-download-the-sample-data.md)

- [第 2 课： 设置教程环境](../r/sqldev-import-data-to-sql-server-using-powershell.md)

- [第 3 课： 浏览和可视化数据形状和分发，通过调用存储过程中的 R 函数](../tutorials/sqldev-explore-and-visualize-the-data.md)

- [第 4 课： 创建数据功能在 T-SQL 的函数中使用 R](../tutorials/sqldev-create-data-features-using-t-sql.md)
  
- [第 5 课： 训练和保存使用函数和存储的过程的 R 模型](../r/sqldev-train-and-save-a-model-using-t-sql.md)
  
- [第 6 课： 在操作化的存储过程包装 R 代码](../tutorials/sqldev-operationalize-the-model.md)。 
  将模型保存到数据库后，使用存储过程从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 调用该模型用于预测。

## <a name="scenario"></a>应用场景

本教程使用的已知的公共数据集，基于在纽约出租车行程。 若要使示例代码更快速地运行，我们创建代表 1%采样的数据。 你将使用此数据来生成预测特定行程是否有可能收到一条提示，或不是，基于例如天、 距离和提取位置的时间的列的二元分类模型。

## <a name="requirements"></a>要求

本教程假定你熟悉基本数据库操作，如创建数据库和表、 导入数据，以及编写 SQL 查询。 它不会假定你知道。在这种情况下，提供了所有 R 代码。 技术精湛的 SQL 程序员可以使用提供的 PowerShell 脚本，在 GitHub 上，示例数据和[!INCLUDE[tsql](../../includes/tsql-md.md)]中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]若要完成此示例。 

在开始本教程： 之前

- 验证是否有的已配置的实例[SQL Server 2016 R Services](../install/sql-r-services-windows-install.md#verify-installation)或[使用 R 启用的 SQL Server 自 2017 年 1 机器学习 Services](../install/sql-machine-learning-services-windows-install.md#verify-installation)。 此外，[确认你拥有的 R 库](../r/determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location)。
- 对于本教程使用的登录名必须有权创建数据库和其他对象，若要上载的数据，选择数据，并运行存储的过程。

> [!NOTE]
> 我们建议你执行**不**使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]编写或测试 R 代码。 如果在存储过程中嵌入的代码没有任何问题，则从存储过程返回的信息是通常不足以了解错误的原因。
> 
> 以进行调试，我们建议你使用工具，如[!INCLUDE[rtvs-short](../../includes/rtvs-short-md.md)]，或 RStudio。 本教程中提供的 R 脚本已使用传统的 R 工具进行开发和调试。

## <a name="next-lesson"></a>下一课

[第 1 课： 下载示例数据](../tutorials/sqldev-download-the-sample-data.md)
