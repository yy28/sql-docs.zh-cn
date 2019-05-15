---
title: 比较用于存储 Blob 的选项 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
ms.assetid: 6038697b-36a9-49e8-a02a-2ad9e2e60e5a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 20d392d5019bf643654bb3a0a6989f882a05b671
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65094219"
---
# <a name="compare-options-for-storing-blobs-sql-server"></a>比较用于存储 Blob 的选项 (SQL Server)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

讨论和比较用于在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中存储文件和文档的选项。

## <a name="Expectations"></a> 在数据库中存储文件 - 好处和期望

很大比例的企业数据本质上是非结构化的，通常作为文件和文档存储在文件系统中。 大多数此类数据由应用程序生成、管理和使用，应用程序通过 Windows API 访问这些文件。 企业通常将此类数据保存在文件系统中，同时将文件的相关元数据存储在关系数据库中。

将非结构化数据集成到关系数据库可提供以下好处：

- 集成的存储和数据管理功能，例如备份。
- 一些集成服务，如针对数据和元数据的全文搜索和语义搜索。
- 易于对非结构化数据的管理和策略管理。

总体而言，难以将这种非结构化数据存储在关系数据库中。 重写现有应用程序（如 Microsoft Word 或 Adobe Reader）以便通过关系数据库 API 进行交互，这种做法并不现实。 这些应用程序希望能够通过 Windows API 访问数据。 应用程序具有以下预期：

- Windows 应用程序并不识别数据库事务，也不需要它们。
- Windows 应用程序要求与文件和目录数据的文件系统 API 兼容。

许多年以前，SQL Server 并未提供任何一种在关系数据库中存储非结构化数据的方法。 而如今却提供了许多存储非结构化数据的方法。

## <a name="Filestream"></a> FILESTREAM

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已有 FILESTREAM 功能。 FILESTREAM 功能为作为文件存储在文件系统中的非结构化数据提供了高效的存储、管理和流式处理方法。 但是，FILESTREAM 解决方案要求自定义的编程，并且不满足上文所述的完全 Windows 应用程序兼容性的要求。

## <a name="FileTables"></a> FileTable

FileTable 功能是在现有 FILESTREAM 功能的基础上生成的。 FileTable 功能使企业客户能够在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中存储非结构化文件数据和目录层次结构。 该功能解决了基于文件的数据的非事务性访问和 Windows 应用程序兼容性的需求。

## <a name="CompareFileTable"></a> FILESTREAM 和 FileTable 的比较

|功能|文件服务器和数据库解决方案|FILESTREAM 解决方案|FileTable 解决方案|
|:------|:--------------------------------|:------------------|:-----------------|
|**用于管理任务的单个存储区**|否|是|**是**|
|**单组服务**：搜索、报告、查询等|否|是|**是**|
|**集成的安全模型**|否|是|**是**|
|**FILESTREAM 数据的就地更新**|是|否|**是**|
|**在数据库中维护文件和目录层次结构**|否|否|**是**|
|**Windows 应用程序兼容性**|是|否|**是**|
|**对文件属性的关系访问**|否|否|**是**|

## <a name="CompareRBS"></a> FILESTREAM 和远程 BLOB 存储区 (RBS) 的比较

另一种用于存储非结构化数据的方法涉及远程 BLOB 存储 (RBS)。 有关详细信息，请参阅[远程 Blob 存储 (RBS) (SQL Server)](remote-blob-store-rbs-sql-server.md)。

## <a name="more"></a> 详细信息

[FILESTREAM (SQL Server)](../../relational-databases/blob/filestream-sql-server.md)  
[FileTables (SQL Server)](../../relational-databases/blob/filetables-sql-server.md)  
[远程 Blob 存储区 (RBS) (SQL Server)](../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)
