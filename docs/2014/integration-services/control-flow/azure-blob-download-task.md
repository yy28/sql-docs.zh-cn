---
title: Azure Blob 下载任务 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpblobdltask.f1
- sql11.dts.designer.afpblobdltask.f1
ms.assetid: 8a63bf44-71be-456d-9a5c-be7c31aff065
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e2f61260b1fceaad3c27a0ce6ab6af28b15582bc
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85433974"
---
# <a name="azure-blob-download-task"></a>Azure Blob 下载任务
  Azure Blob 下载任务启用了一个 SSIS 包来从 Azure blob 存储区下载文件。   
若要添加 **Azure Blob 下载任务**，可将其拖放到 SSIS 设计器，然后双击或右键单击“编辑”，以查看以下“Azure Blob 下载任务编辑器”对话框   。  
  
 下表提供了此对话框中的字段说明。  
  
|||  
|-|-|  
|**字段**|**说明**|  
|AzureStorageConnection|选择一个现有的 Azure 存储连接管理器或创建一个新的连接管理器，用于引用指向在其中托管 blob 文件的 Azure 存储帐户。|  
|BlobContainer|指定包含要下载的 blob 文件的 blob 容器的名称。|  
|BlobDirectory|指定包含要下载的 blob 文件的 blob 目录。 该 blob 目录是一个虚拟层次结构。|  
|LocalDirectory|指定将在其中存储下载的 blob 文件的本地目录。|  
|FileName|指定名称筛选器以选择具有指定名称模式的文件。 例如 MySheet*.xls\* 包括如 MySheet001.xls 和 MySheetABC.xlsx 等文件。|  
|TimeRangeFrom/TimeRangeTo|指定时间范围筛选器。 包括介于 **TimeRangeFrom** 和 **TimeRangeTo** 之间修改的文件。|  
  
  
