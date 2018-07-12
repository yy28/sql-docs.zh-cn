---
title: 比较用于存储 Blob 的选项 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: filestream
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6038697b-36a9-49e8-a02a-2ad9e2e60e5a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a622ad290a00a58c3fb0d0e4003e291a7ba77d3b
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37421106"
---
# <a name="compare-options-for-storing-blobs-sql-server"></a>比较用于存储 Blob 的选项 (SQL Server)
  讨论和比较用于在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中存储文件和文档的选项。  
  
##  <a name="Expectations"></a> 在数据库中存储文件 - 好处和期望  
 很大比例的企业数据本质上是非结构化的，通常作为文件和文档存储在文件系统中。 大多数此类数据由应用程序生成、管理和使用，应用程序通过 Windows API 访问这些文件。 企业通常将此类数据保存在文件系统中，同时将文件的相关元数据存储在关系数据库中。  
  
 将非结构化数据集成到关系数据库可提供很多好处。 其中包括：  
  
-   集成的存储和数据管理功能，例如备份。  
  
-   一些集成服务，如针对数据和元数据的全文搜索和语义搜索。  
  
-   易于对非结构化数据的管理和策略管理。  
  
 但对于大部分企业而言，难以将这种非结构化数据存储在关系数据库中。 以前不能在关系型系统上运行基于 Windows 的现有应用程序。 重写现有应用程序（如 Microsoft Word 或 Adobe Reader）以便在关系数据库 API 上运行并不现实。 这些应用程序只是希望能够通过 Windows API 访问数据。 换而言之，要求做到以下几点：  
  
-   Windows 应用程序并不识别数据库事务，也不需要它们。  
  
-   Windows 应用程序要求与文件和目录数据的文件系统 API 兼容。  
  
##  <a name="Filestream"></a> FILESTREAM  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已有 FILESTREAM 功能，它为作为文件存储在文件系统中的非结构化数据提供了高效的存储、管理和流式处理方法。 但是，FILESTREAM 解决方案要求自定义的编程，并且不满足上文所述的完全 Windows 应用程序兼容性的要求。  
  
##  <a name="FileTables"></a> FileTable  
 FileTable 功能以现有的 FILESTREAM 功能为基础，使企业客户只要满足对基于文件的数据的非事务性访问和 Windows 应用程序兼容性要求，就可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中存储非结构化文件数据和目录层次结构。  
  
##  <a name="CompareFileTable"></a> FILESTREAM 和 FileTable 的比较  
  
|功能|文件服务器和数据库解决方案|FILESTREAM 解决方案|FileTable 解决方案|  
|-------------|---------------------------------------|-------------------------|------------------------|  
|**用于管理任务的单个存储区**|“否”|是|**是**|  
|**单组服务**：搜索、报告、查询等|“否”|是|**是**|  
|**集成的安全模型**|“否”|是|**是**|  
|**FILESTREAM 数据的就地更新**|是|“否”|**是**|  
|**在数据库中维护文件和目录层次结构**|“否”|“否”|**是**|  
|**Windows 应用程序兼容性**|是|“否”|**是**|  
|**对文件属性的关系访问**|“否”|“否”|**是**|  
  
##  <a name="CompareRBS"></a> FILESTREAM 和远程 BLOB 存储区 (RBS) 的比较  
 有关这两种功能的比较，请参阅来自 RBS 团队的以下博客： [SQL Server 远程 BLOB 存储区和 FILESTREAM 功能比较](http://go.microsoft.com/fwlink/?LinkId=210317)。  
  
##  <a name="more"></a> 详细信息  
 [FILESTREAM (SQL Server)](filestream-sql-server.md)  
 [FileTables (SQL Server)](filetables-sql-server.md)  
 [远程 Blob 存储区 (RBS) (SQL Server)](remote-blob-store-rbs-sql-server.md)  
  
