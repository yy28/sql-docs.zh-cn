---
title: "Azure blob 源 | Microsoft Docs"
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
  - "sql13.dts.designer.afpblobsrc.f1"
  - "sql14.dts.designer.afpblobsrc.f1"
ms.assetid: 80645c5c-88c8-4fb0-8607-de1bb7bffcbb
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Azure blob 源
  借助“Azure blob 源”  组件，SSIS 包可以读取 Azure blob 中的数据。 支持的文件格式：CSV 和 AVRO。
  
>   [!NOTE] 若要确保 Azure 存储连接管理器和使用它的组件（即 Blob 源、Blob 目标、Blob 上传任务和 Blob 下载任务）可以连接到常规用途的存储帐户和 Blob 存储帐户，请确保[在此处](https://www.microsoft.com/download/details.aspx?id=49492)下载最新版本的 Azure 功能包。 有关这两种类型的存储帐户的详细信息，请参阅 [Microsoft Azure 存储空间简介](https://azure.microsoft.com/en-us/documentation/articles/storage-introduction/#general-purpose-storage-accounts)。
  
  若要查看 Azure blob 源的编辑器，请将“Azure blob 源”拖放到数据流设计器上，然后双击它打开编辑器。  
  
 “Azure blob 源”是适用于 Azure for SQL Server 2016 的 SQL Server Integration Services (SSIS) 功能包组件。 从 [此处](http://go.microsoft.com/fwlink/?LinkID=626967)下载功能包。  
  
1.  对于“Azure 存储空间连接管理器”  字段，请指定一个现有的 Azure 存储空间连接管理器，或新建一个引用 Azure 存储空间帐户的连接管理器。  
  
2.  对于“blob 容器名称”  字段，请指定包含源文件的 blob 容器的名称。  
  
3.  对于“blob 名称”  字段，请指定 blob 的路径。  
  
4.  对于“blob 文件格式”  字段，请指定要使用的 blob 格式。  
  
5.  如果文件格式是 CSV，你必须指定“列分隔符字符”  值。 此外，如果文件中的第一行包含列名称，请选择“在第一个数据行中显示列名称”  。  
  
6.  指定连接信息后，切换到“列”  页，将源列映射到 SSIS 数据流的目标列。  
  
  