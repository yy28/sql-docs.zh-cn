---
title: 部署 Azure Data Studio 笔记本 SQL Server 大数据群集
titleSuffix: Deploy SQL Server big data cluster cluster with Azure Data Studio notebooks
description: 使用 Azure Data Studio 中的笔记本部署大数据群集。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f12a4f06ceb1c3a48b2b2fc661c59594e6d6cce3
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426417"
---
# <a name="deploy-sql-server-big-data-cluster-with-azure-data-studio-notebooks"></a>部署 Azure Data Studio 笔记本 SQL Server 大数据群集

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]为包含部署笔记本的 Azure Data Studio 提供扩展。 部署笔记本包含可以在 Azure Data Studio 中使用的文档和代码, 以创建 SQL Server 大数据群集。 

已最初实现为开源项目,[笔记本](notebooks-guidance.md)已实现到[Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download)。 可以将 markdown 用于文本单元中的文本和一个可用内核, 以在代码单元中编写代码。

你可以使用笔记本为部署大数据群集[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]。

## <a name="prerequisites"></a>先决条件
若要启动笔记本, 需要满足以下先决条件:

* 已安装[Azure Data Studio](http://docs.microsoft.com/sql/azure-data-studio/download)的最新版本
* [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]Azure Data Studio 中安装的扩展

除此之外, 部署 SQL Server 2019 大数据群集也需要:

* [azdata](deploy-install-azdata.md)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management)
* [Azure CLI](/cli/azure/install-azure-cli)

## <a name="launch-the-notebook"></a>启动笔记本

1. 安装并启动[Azure Data Studio 预览体验内部版本](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)。
1.  在 "**连接**" 选项卡上, 单击 " **...** ", 然后选择 "**部署 SQL Server 大数据群集 ...** "。

   ![AI 和 ML](media/deploy-notebooks/deploy-notebooks-1.png)

1. 从**部署目标**的 "**选项**" 下, 选择 "**新建 azure Kubernetes 群集**" 或 "**现有 azure Kubernetes Service 群集**"。
1. 选择 "**打开笔记本**"。

此操作会启动相应的笔记本。 若要完成部署, 请按照笔记本中的说明在现有的或新的 Azure [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Kubernetes 服务群集上部署大数据群集。
