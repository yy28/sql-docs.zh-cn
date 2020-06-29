---
title: Azure Blob 上载任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpblobuptask.f1
- sql11.dts.designer.afpblobuptask.f1
ms.assetid: 6ea068b0-4cd8-45b5-b89d-09b8f25040c0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0ca15c5a77a2694293981121f4e5927be8ec0e1c
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85433934"
---
# <a name="azure-blob-upload-task"></a>Azure blob 上载任务
  “Azure blob 上载任务”可让 SSIS 包将文件上载到 Azure blob 存储区中。   
若要添加“Azure blob 上传任务”  ，请将其拖放到“SSIS 设计器”中，双击或右键单击它，然后单击“编辑”  调出下面的“Azure blob 上传任务编辑器”  对话框。  
  
 下表介绍了此对话框中的各个字段。  
  
|||  
|-|-|  
|**字段**|**说明**|  
|AzureStorageConnection|选择一个现有的 Azure 存储连接管理器或创建一个新的连接管理器，用于引用指向在其中托管 blob 文件的 Azure 存储帐户。|  
|BlobContainer|指定将上载的文件作为 blob 保留的 blob 容器的名称。|  
|BlobDirectory|指定将上载的文件作为块 blob 存储的 blob 目录。 该 blob 目录是一个虚拟层次结构。 如果 blob 已存在，它会被替换。|  
|LocalDirectory|指定包含要上载的文件的本地目录。|  
|FileName|指定名称筛选器以选择具有指定名称模式的文件。 例如 MySheet*.xls\* 包括如 MySheet001.xls 和 MySheetABC.xlsx 等文件。|  
|TimeRangeFrom/TimeRangeTo|指定时间范围筛选器。 包括介于 **TimeRangeFrom** 和 **TimeRangeTo** 之间修改的文件。|  
  
  
