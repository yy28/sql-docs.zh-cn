---
title: 管理 Azure Data Studio 笔记本 SQL Server 大数据群集
titleSuffix: Manage SQL Server big data cluster cluster with Azure Data Studio notebooks
description: 使用 Azure Data Studio 中的笔记本来管理大数据群集并对其进行故障排除。
author: yualan
ms.author: alanyu
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8d87b09878539cccd40191d870bf97487579dca2
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426397"
---
# <a name="manage-big-data-clusters-for-sql-server-with-azure-data-studio-notebooks"></a>管理 Azure Data Studio 笔记本 SQL Server 的大数据群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]为包含部署笔记本的 Azure Data Studio 提供扩展。 部署笔记本包含可在 Azure Data Studio 中使用的文档和代码, 用于管理 SQL Server 的大数据群集。

已最初实现为开源项目,[笔记本](notebooks-guidance.md)已实现到[Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download)。 可以将 markdown 用于文本单元中的文本和一个可用内核, 以在代码单元中编写代码。

你可以使用笔记本为部署大数据群集[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]。

## <a name="prerequisites"></a>系统必备

若要启动笔记本, 需要满足以下先决条件:

* 最新版本的[Azure Data Studio 预览体验内部](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)版本
* [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]Azure Data Studio 中安装的扩展

除此之外, 部署 SQL Server 2019 大数据群集也需要:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)
