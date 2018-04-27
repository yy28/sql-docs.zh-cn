---
title: Azure Blob 下载任务 | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2016
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.afpblobdltask.f1
- sql14.dts.designer.afpblobdltask.f1
ms.assetid: 8a63bf44-71be-456d-9a5c-be7c31aff065
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1c8288d8b83fe0887f5d332871569119990ea4b4
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="azure-blob-download-task"></a>Azure Blob 下载任务
Azure Blob 下载任务启用了一个 SSIS 包来从 Azure blob 存储区下载文件。

若要添加 **Azure Blob 下载任务**，可将其拖放到 SSIS 设计器，然后双击或右键单击“编辑”，以查看以下“Azure Blob 下载任务编辑器”对话框。  
  
 “Azure Blob 下载任务”是[适用于 Azure 的 SQL Server Integration Services (SSIS) 功能包](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)组件。  
  
 下表提供了此对话框中的字段说明。  
  
|||  
|-|-|  
|**字段**|**Description**|  
|AzureStorageConnection|选择一个现有的 Azure 存储连接管理器或创建一个新的连接管理器，用于引用指向在其中托管 blob 文件的 Azure 存储帐户。|  
|BlobContainer|指定包含要下载的 blob 文件的 blob 容器的名称。|  
|BlobDirectory|指定包含要下载的 blob 文件的 blob 目录。 Blob 目录是虚拟的层次结构。|  
|LocalDirectory|指定用于存储下载的 blob 文件的本地目录。|  
|FileName|指定用于选择具有指定名称模式的文件的名称筛选器。 例如，`MySheet*.xls\*` 包括 `MySheet001.xls` 和 `MySheetABC.xlsx` 等文件。|  
|TimeRangeFrom/TimeRangeTo|指定时间范围筛选器。 将包括在 **TimeRangeFrom** 之后以及 **TimeRangeTo** 之前修改的文件。|  
  
  
