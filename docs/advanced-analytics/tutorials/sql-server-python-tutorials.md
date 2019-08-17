---
title: Python 教程
description: 本文介绍适用于 SQL Server 机器学习服务的 Python 教程。 了解如何运行 Python 脚本。 构建、培训 Python 模型并将其部署到 SQL Server。 了解远程和本地计算上下文。 探索用于数据科学和机器学习的 Microsoft Python 包。
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/16/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 238249ae90556d342e9c6cd50e568d65ff1cb6f6
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553174"
---
# <a name="python-tutorials-for-sql-server-machine-learning-services"></a>适用于 SQL Server 机器学习服务的 Python 教程
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍适用于[SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)的 Python 教程。 

+ 了解如何运行 Python 脚本。
+ 构建、培训 Python 模型并将其部署到 SQL Server。
+ 了解远程和本地计算上下文。
+ 探索用于数据科学和机器学习的 Microsoft Python 包。

<a name="bkmk_pythontutorials"></a>

## <a name="python-quickstarts-and-tutorials"></a>Python 快速入门和教程

| 链接 | 描述 |
|------|-------------|
| [快速入门：SQL Server 中的 "Hello world" Python 脚本](quickstart-python-run-using-t-sql.md) | 了解如何在 T-sql 中调用 Python 的基本知识。 |
| [快速入门：使用中的存储过程创建、定型和使用 Python 模型 SQL Server](quickstart-python-train-score-in-tsql.md) | 说明在存储过程中嵌入 Python 代码、提供输入和存储过程执行的机制。 |
| [教程：使用 revoscalepy 创建模型](use-python-revoscalepy-to-create-model.md) | 演示如何使用 SQL Server 计算上下文从远程 Python 终端运行代码。 你应该对 Python 工具和环境有一定的了解。 提供了示例代码, 该代码使用**rxLinMod**从新的**revoscalepy**库创建模型。 |
| [教程：了解面向 SQL 开发人员的数据库内 Python 分析](sqldev-in-database-python-for-sql-developers.md) | 本端到端演练演示了使用 T-sql 存储过程构建完整 Python 解决方案的过程。 所有 Python 代码都包括在内。|

## <a name="see-also"></a>请参阅

+ [要 SQL Server 的 Python 扩展](../concepts/extension-python.md)
+ [SQL Server 机器学习服务教程](machine-learning-services-tutorials.md)
