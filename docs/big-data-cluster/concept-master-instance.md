---
title: 主实例是什么？
titleSuffix: SQL Server 2019 big data clusters
description: 本指南介绍了 SQL Server 2019 大数据群集 （预览版） 中的 SQL Server 主实例。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 9c3809e481e00c94f01c1968a82638df3e37f80f
ms.sourcegitcommit: 715683b5fc7a8e28a86be8949a194226b72ac915
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/26/2019
ms.locfileid: "58477943"
---
# <a name="what-is-the-master-instance-in-a-sql-server-2019-big-data-cluster"></a>什么是 SQL Server 2019 大数据群集中的主实例？

本文介绍的角色*SQL Server 主实例*SQL Server 2019 大数据群集中。 主实例是 SQL Server 大数据群集中运行的 SQL Server 实例[控制平面](big-data-cluster-overview.md#controlplane)。

SQL Server 主实例提供了以下功能：

## <a name="connectivity"></a>连接

SQL Server 主实例为群集提供从外部访问 TDS 端点。 应用程序或 Azure Data Studio 之类的 SQL Server 工具可以连接或到此终结点，就像您一样的 SQL Server Management Studio 将任何其他 SQL Server 实例。

## <a name="scale-out-query-management"></a>横向扩展查询管理

SQL Server 主实例包含用于将查询分发中的节点上的 SQL Server 实例之间的横向扩展查询引擎[计算池](concept-compute-pool.md)。 横向扩展查询引擎还提供通过 TRANSACT-SQL 访问权限而无需任何其他配置群集中的所有 Hive 表。

## <a name="metadata-and-user-databases"></a>元数据和用户数据库

除了标准的 SQL Server 系统数据库，SQL 主控实例还包含以下元素：

- 元数据数据库中承载的 HDFS 表元数据
- 数据平面分片映射
- 提供群集数据平面访问权限的外部表的详细信息。
- PolyBase 外部数据源和外部表定义在用户数据库中。

您还可以选择将用户数据库添加到 SQL Server 主实例。

## <a name="machine-learning-services"></a>机器学习服务

SQL Server 机器学习服务是一项附加功能到数据库引擎，用于在 SQL Server 中执行 Java、 R 和 Python 代码。 此功能基于 SQL Server 可扩展性框架，这将从核心引擎进程的外部进程中隔离出来，但完全集成，与关系数据作为存储过程、 包含 R 或 Python 语句的 T-SQL 脚本或 Java、 R 或包含 T-SQL 的 Python 代码。

作为 SQL Server 大数据群集的一部分，机器学习服务将在默认情况下的 SQL Server 主实例上可用。 这意味着，一旦 SQL Server 主实例上启用了外部脚本执行，将为可能要执行 Java 中，使用 sp_execute_external_script 的 R 和 Python 脚本。

### <a name="advantages-of-machine-learning-services-in-a-big-data-cluster"></a>大数据群集中的机器学习服务的优点

SQL Server 2019 简化大数据来联接到维度的数据通常存储在企业数据库。 大数据的值会大大提高时它不只是在手中的部分的组织，但也包含在报表、 仪表板和应用程序。 同时，数据科学家可以继续使用 Spark/HDFS 生态系统工具和过程简单，有权在 SQL Server 主实例和可访问的外部数据源中的数据访问实时_通过_SQL Server master实例。

使用 SQL Server 2019 大数据群集时，您可以做更多与你的企业数据湖。 SQL Server 开发人员和分析师可以：

* 生成应用程序使用来自企业 data lake 数据。
* 使用 Transact SQL 查询的所有数据的原因。
* 使用 SQL Server 工具和应用程序的现有生态系统访问和分析企业数据。
* 减少数据移动到数据虚拟化和数据市场的需要。
* 继续针对大数据方案中使用 Spark。
* 构建智能的企业应用程序使用 Spark 或 SQL Server 通过 data lake 定型的模型。
* 操作在为获得最佳性能的生产数据库中的模型。
* Stream 数据直接到企业数据集市、 供实时分析。
* 浏览交互式分析和 BI 工具直观地使用的数据。

## <a name="next-steps"></a>后续步骤

若要了解有关 SQL Server 大数据群集的详细信息，请参阅以下资源：

- [什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)
- [研讨会：Microsoft SQL Server 大数据群集体系结构](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
