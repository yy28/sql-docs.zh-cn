---
title: "Azure Blob 下载任务 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "07/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.afpblobdltask.f1"
  - "sql14.dts.designer.afpblobdltask.f1"
ms.assetid: 8a63bf44-71be-456d-9a5c-be7c31aff065
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 12
---
# Azure Blob 下载任务
  Azure Blob 下载任务启用了一个 SSIS 包来从 Azure blob 存储区下载文件。

>   [!NOTE] 若要确保 Azure 存储连接管理器和使用它的组件（即 Blob 源、Blob 目标、Blob 上传任务和 Blob 下载任务）可以连接到常规用途的存储帐户和 Blob 存储帐户，请确保[在此处](https://www.microsoft.com/download/details.aspx?id=49492)下载最新版本的 Azure 功能包。 有关这两种类型的存储帐户的详细信息，请参阅 [Microsoft Azure 存储空间简介](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts)。
   
若要添加 **Azure Blob 下载任务**，可将其拖放到 SSIS 设计器，然后双击或右键单击“编辑”，以查看以下“Azure Blob 下载任务编辑器”对话框。  
  
 “Azure Blob 下载任务”是适用于 Azure for SQL Server 2016 的 SQL Server Integration Services (SSIS) 功能包的组成部分。 从 [此处](http://go.microsoft.com/fwlink/?LinkID=626967)下载功能包。  
  
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
  
  