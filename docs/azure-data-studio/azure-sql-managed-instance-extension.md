---
title: Azure SQL 托管实例扩展
titleSuffix: Azure Data Studio
description: 将 Azure Data Studio 与 Azure SQL 托管实例结合使用
ms.custom: seodec18
ms.date: 10/07/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: jovanpop-msft
ms.author: jovanpop
manager: alanyu
ms.openlocfilehash: d443292fb091679d3d6a18d557a5a7aac464fdec
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041138"
---
# <a name="managed-instance-support-for-azure-data-studio-preview"></a>Azure Data Studio 的托管实例支持（预览版）

此扩展可用于在 [Azure Data Studio](https://github.com/Microsoft/azuredatastudio) 中使用 [Azure SQL 托管实例](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-index)。 此扩展提供以下功能：

- 显示托管实例的属性（vCore，已用存储）。
- 在过去两小时内监视 CPU 和存储使用情况。
- 显示配置警告和优化建议。
- 显示数据库副本的状态。
- 显示已筛选的错误日志。

## <a name="installations"></a>安装

可以按照 [Azure Data Studio 文档](https://docs.microsoft.com/sql/azure-data-studio/extensions)中的步骤安装托管实例扩展的官方版本。
在“扩展”窗格中，搜索“托管实例”扩展并将其安装在此处。  未来有任何扩展更新，你都会收到系统自动发送的消息！

安装托管实例扩展后，Azure Data Studio 中将显示 `Managed Instance` 选项卡。 在此选项卡上，可以找到特定于托管实例的信息。

## <a name="properties"></a>属性

此扩展可用于查看托管实例的技术特征和某些资源使用情况。

![托管实例属性](media/azure-sql-mi-extension/ads-mi-tab1.png)

在第一个边栏选项卡上，可以看到以下详细信息：

- **基本属性**，例如 vCore、内存、存储、当前服务层和硬件生成的可用数目，以及 IO 特征（如实例日志写入吞吐量或文件 IO/吞吐量特征）。
- **本地 SSD 存储的使用情况**。 在常规用途服务层上，只有 TEMPDB 文件会在放置本地，而在业务关键层上，所有数据库文件都会放置在本地 SSD 存储上。 在本部分中，可以查看托管实例使用的本地存储空间。
- **Azure 高级磁盘存储的使用情况** - 常规用途服务层中的用户和系统数据库会放置在 Azure 高级存储上。 可在此处找到已使用的数据量，以及剩余的存储和文件数。 在业务关键服务层上，此部分为空。
- **资源使用情况**，将显示你的实例在过去两小时内使用的存储空间和 CPU 量。 如果达到限制，请增大实例大小。

## <a name="recommendations"></a>建议

此扩展提供一些建议和警报，可帮助你优化托管实例。

![托管实例建议](media/azure-sql-mi-extension/ads-mi-tab2.png)

此表中所示的某些建议如下：

- 达到存储空间限制 - 应删除不必要的数据或增大实例存储大小，因为达到存储限制的数据库可能无法处理查询，甚至无法读取查询。
- 达到实例吞吐量限制 - 如果要在 GP 上加载 ~22MB/s 或在 BC 上加载 ~48 MB/s，托管实例会限制你的负荷以确保可以执行备份。
- 内存压力 - 低页生存期或大量 `PAGEIOLATCH` 等待统计信息可能表明实例正在从内存中退出页面，并不断尝试从磁盘加载更多页面。
- 日志文件限制 - 如果日志达到了[常规用途服务层上的文件 IO 限制](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-resource-limits#file-io-characteristics-in-general-purpose-tier)，则可能需要增大文件大小以获得更好的性能。
- 数据文件限制 - 如果数据文件达到了[常规用途服务层上的文件 IO 限制](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-resource-limits#file-io-characteristics-in-general-purpose-tier)，则可能需要增大文件大小以获得更好的性能。 此问题可能会导致内存压力并降低备份速度。
- 可用性问题 - 如果进程失败，则大量虚拟日志文件可能会导致性能降低，并且可能会使常规用途服务层上的数据库恢复时间更长。

应定期查看这些建议，调查根本原因，并采取纠正措施。 托管实例扩展提供了一些脚本，可以执行这些脚本来缓解已报告的某些问题。

## <a name="replicas"></a>副本

托管实例扩展可用于查看托管实例中的数据库副本状态。

![托管实例副本](media/azure-sql-mi-extension/ads-mi-tab3.png)

在常规用途服务层上，每个数据库都有一个（主）副本，而在业务关键实例上，每个数据库都有一个主副本和三个次要副本（其中一个用于只读工作负荷）。 可在此处监视同步过程，并验证所有次要副本是否与主副本同步。

## <a name="logs"></a>日志

托管实例扩展显示最相关的最新 SQL 错误日志条目。

![托管实例日志条目](media/azure-sql-mi-extension/ads-mi-tab4.png)

托管实例会发出大量日志条目，其中大多数日志条目是内部/系统信息。 一些日志条目显示的是物理数据库名称（`GUID` 值），而不是实际逻辑数据库名称。

托管实例扩展基于 [Dimitri Furman 方法](https://techcommunity.microsoft.com/t5/DataCAT/Azure-SQL-DB-Managed-Instance-sp-readmierrorlog/ba-p/305506)筛选出不必要的日志条目，并显示实际逻辑文件名而不是物理名称。

## <a name="reporting-problems"></a>报告问题

如果托管实例扩展遇到任何问题，请在[扩展 GitHub 项目](https://github.com/JocaPC/AzureDataStudio-Managed-Instance/issues)上报告问题。

## <a name="maintainers"></a>维护人员

- [Jovan Popovic(MSFT)](https://github.com/jovanpop_msft) - [@jovanpop_msft](https://twitter.com/JovanPop_MSFT)

## <a name="code-of-conduct"></a>行为准则

此项目采用了 [Microsoft 开放源代码行为准则][conduct-code]。
有关详细信息，请参阅[行为准则常见问题解答][conduct-FAQ]，如有任何其他问题或评论，请联系 [opencode@microsoft.com][conduct-email]。

[conduct-code]: http://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: http://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com
[conduct-md]: https://github.com/PowerShell/vscode-powershell/blob/master/CODE_OF_CONDUCT.md
