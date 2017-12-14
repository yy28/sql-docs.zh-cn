---
title: "在本地和 Azure 中存储和检索文件共享上的文件 | Microsoft Docs"
description: "本文介绍如何将本地和 Azure 中的文件系统和文件共享与 SSIS 结合使用。"
ms.date: 11/10/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f4980f39deea4d70817da3650dccbff7997ba83d
ms.sourcegitcommit: 06bb91d138a4d6395c7603a2d8f99c69a20642d3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/16/2017
---
# <a name="store-and-retrieve-files-on-file-shares-on-premises-and-in-azure-with-ssis"></a>借助 SSIS 存储和检索本地和 Azure 中文件共享上的文件
本文介绍将使用本地文件系统的包提升和迁移到 Azure 中的 SSIS 时，如何更新 SQL Server Integration Services (SSIS) 包。

> [!IMPORTANT]
> 目前，SSIS 目录数据库 (SSISDB) 仅支持一组访问凭据。 因此 Azure-SSIS Integration Runtime (IR) 不能使用不同的凭证连接到多个本地文件共享和 Azure 文件共享。

## <a name="store-temporary-files"></a>存储临时文件
如果在单个包执行期间需存储和处理临时文件，包可以使用 Azure-SSIS Integration Runtime 节点的临时文件夹 `(.)/temp` 或 `%TEMP%`。

## <a name="store-files-across-multiple-package-executions"></a>跨多个包执行操作存储文件
如果需要存储和处理永久性文件并跨多个包执行保存它们，可以使用本地文件共享或 Azure 文件。

### <a name="use-on-premises-file-shares"></a>使用本地文件共享
要在将使用本地文件系统的包提升和迁移到 Azure 中的 SSIS 时继续使用本地文件共享，请执行以下操作：
1.  将文件从本地文件系统传输到本地文件共享。
2.  将本地文件共享联接到 Azure 虚拟网络 (VNet)。
3.  将 Azure-SSIS IR 联接到同一个 VNet。 有关详细信息，请参阅[将 Azure-SSIS 集成运行时联接到虚拟网络](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network)。
4.  通过设置使用 Windows 身份验证的访问凭据，将 Azure-SSIS IR 连接到同一个 VNet 内的本地文件共享。 有关详细信息，请参阅[使用 Windows 身份验证连接到本地数据源和 Azure 文件共享](ssis-azure-connect-with-windows-auth.md)。
5.  将包中的本地文件路径更新为指向本地文件共享的 UNC 路径。 例如，将 `C:\abc.txt` 更新为 `\\<on-prem-server-name>\<share-name>\abc.txt`。

### <a name="use-azure-file-shares"></a>使用 Azure 文件共享
若直接迁移将本地文件系统使用到 Azure 中 SSIS 时要使用 Azure 文件，请执行以下操作：
1.  将本地文件系统的文件传输到 Azure 文件。 有关详细信息，请参阅 [Azure 文件](https://azure.microsoft.com/services/storage/files/)。
2.  通过设置使用 Windows 身份验证的访问凭据，将 Azure-SSIS IR 连接到 Azure 文件。 有关详细信息，请参阅[使用 Windows 身份验证连接到本地数据源和 Azure 文件共享](ssis-azure-connect-with-windows-auth.md)。
3.  更新包中的本地文件路径到指向 Azure 文件的 UNC 路径。 例如，将 `C:\abc.txt` 更新为 `\\<storage-account-name>.file.core.windows.net\<share-name>\abc.txt`。
