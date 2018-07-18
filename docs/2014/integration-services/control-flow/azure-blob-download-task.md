---
title: Azure Blob 下载任务 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpblobdltask.f1
- sql11.dts.designer.afpblobdltask.f1
ms.assetid: 8a63bf44-71be-456d-9a5c-be7c31aff065
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d6825d61a997969691405f312eb91afd8b514087
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37287673"
---
# <a name="azure-blob-download-task"></a>Azure Blob 下载任务
  Azure Blob 下载任务启用了一个 SSIS 包来从 Azure blob 存储区下载文件。   
若要添加 **Azure Blob 下载任务**，可将其拖放到 SSIS 设计器，然后双击或右键单击“编辑”，  以查看以下 **Azure Blob 下载任务编辑器** 对话框。  
  
 下表提供了此对话框中的字段说明。  
  
|||  
|-|-|  
|**字段**|**Description**|  
|AzureStorageConnection|选择一个现有的 Azure 存储连接管理器或创建一个新的连接管理器，用于引用指向在其中托管 blob 文件的 Azure 存储帐户。|  
|BlobContainer|指定包含要下载的 blob 文件的 blob 容器的名称。|  
|BlobDirectory|指定包含要下载的 blob 文件的 blob 目录。 Blob 目录是虚拟的层次结构。|  
|LocalDirectory|指定将在其中存储下载的 blob 文件的本地目录。|  
|FileName|指定用于选择具有指定名称模式的文件的名称筛选器。 例如 MySheet*.xls\* 包括如 MySheet001.xls 和 MySheetABC.xlsx 等文件。|  
|TimeRangeFrom/TimeRangeTo|指定时间范围筛选器。 包括介于 **TimeRangeFrom** 和 **TimeRangeTo** 之间修改的文件。|  
  
  
