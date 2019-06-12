---
title: 灵活的文件任务 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPEXTFILETASK.F1
- SQL14.DTS.DESIGNER.AFPEXTFILETASK.F1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2d01304a36f7676f53ffef3f6c6e3c600cb87cb6
ms.sourcegitcommit: fc0eb955b41c9c508a1fe550eb5421c05fbf11b4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66411094"
---
# <a name="flexible-file-task"></a>灵活的文件任务

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

通过灵活的文件任务，用户可在各种支持的存储服务上执行文件操作。
当前支持的存储服务为

- 本地文件系统
- [Azure Blob 存储](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-introduction)

灵活的文件任务是[适用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)的组成部分。

要将灵活的文件任务添加到包，请将其从 SSIS 工具箱拖到设计器画布。 然后，双击该任务，或右键单击任务并选择“编辑”，以打开“灵活的文件任务编辑器”对话框   。

“操作”属性指定要执行的文件操作  。
目前仅支持“复制”操作  。

以下属性可用于“复制”操作  。

- **SourceConnectionType：** 指定源连接管理器类型。
- **SourceConnection：** 指定源连接管理器。
- **SourceFolderPath：** 指定源文件夹路径。
- **SourceFileName：** 指定源文件名称。 如果留空，则将复制源文件夹。
- **SearchRecursively：** 指定是否以递归方式复制子文件夹。
- **DestinationConnectionType：** 指定目标连接管理器类型。
- **DestinationConnection：** 指定目标连接管理器。
- **DestinationFolderPath：** 指定目标文件夹路径。
- **DestinationFileName：** 指定目标文件名称。
