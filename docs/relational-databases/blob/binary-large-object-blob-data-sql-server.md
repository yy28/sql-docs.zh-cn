---
title: 二进制大型对象 (Blob) 数据 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.technology: filestream
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], design and implementation
ms.assetid: 97509274-c3f8-43e5-a37c-52f1ffe0961a
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0e5118f2a40e99ad9a46d0027cc3c6a860306f91
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2018
ms.locfileid: "36760392"
---
# <a name="binary-large-object-blob-data-sql-server"></a>二进制大型对象 (Blob) 数据 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供用于在数据库中或远程存储设备上存储文件和文档的解决方案。  
  
## <a name="compare-options-for-storing-blobs-in-sql-server"></a>比较用于在 SQL Server 中存储 Blob 的选项

比较 FILESTREAM、FileTable 和远程 Blob 存储区的优劣 请参阅[比较用于存储 Blob 的选项 (SQL Server)](../../relational-databases/blob/compare-options-for-storing-blobs-sql-server.md)。
  
##  <a name="options-for-storing-blobs"></a>用于存储 Blob 的选项  

### <a name="filestream-40sql-server41relational-databasesblobfilestream-sql-servermd"></a>[FILESTREAM (SQL Server)](../../relational-databases/blob/filestream-sql-server.md)  

借助 FILESTREAM，基于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的应用程序可以将非结构化的数据（如文档和图像）存储在文件系统中。 应用程序在利用丰富的流式 API 和文件系统的性能的同时，还可保持非结构化数据和对应的结构化数据之间的事务一致性。  
  
### <a name="filetables-40sql-server41relational-databasesblobfiletables-sql-servermd"></a>[FileTables (SQL Server)](../../relational-databases/blob/filetables-sql-server.md)  

FileTable 功能为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中存储的文件数据提供对 Windows 文件命名空间的支持以及与 Windows 应用程序的兼容性支持。 FileTable 使得应用程序可以集成其存储和数据管理组件，可对非结构化数据和元数据提供集成的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务（包括全文搜索和语义搜索）。  
  
 换言之，您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中将文件和文档存储在称作 FileTable 的特别的表中，但是从 Windows 应用程序访问它们，就好像它们存储在文件系统中，而不必对您的客户端应用程序进行任何更改。  
  
### <a name="remote-blob-store-40rbs41-40sql-server41relational-databasesblobremote-blob-store-rbs-sql-servermd"></a>[远程 Blob 存储区 (RBS) (SQL Server)](../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的远程 BLOB 存储 (RBS) 使数据库管理员能够在商用存储解决方案中存储二进制大型对象 (BLOB)，而不是直接存储在服务器上。 这可以节省大量空间，避免浪费昂贵的服务器硬件资源。 RBS 提供一组可定义应用程序标准化模型的 API 库以访问 BLOB 数据。 RBS 还包含维护工具（如垃圾收集）以帮助管理远程 BLOB 数据。  
  
 RBS 包括在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装介质上，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序不安装它。  
  
  
