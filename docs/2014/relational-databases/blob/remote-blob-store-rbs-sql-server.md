---
title: 远程 Blob 存储 (RBS) (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.technology: filestream
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Remote Blob Store (RBS) [SQL Server]
- RBS (Remote Blob Store) [SQL Server]
ms.assetid: 31c947cf-53e9-4ff4-939b-4c1d034ea5b1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4379e0ff3ca534acd6ae130cbdf0f8acd2b6a81f
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2019
ms.locfileid: "66009852"
---
# <a name="remote-blob-store-rbs-sql-server"></a>远程 Blob 存储区 (RBS) (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 远程 BLOB 存储区 (RBS) 是一个可选的附加组件，它允许数据库管理员在商用存储解决方案中存储二进制大型对象，而不是直接存储在主数据库服务器上。  
  
 RBS 包括在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装介质上，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序不安装它。  
  
 有关 RBS 的详细信息，请参阅本主题中的 [RBS 资源](#rbsresources) 。  
  
## <a name="benefits-of-rbs"></a>RBS 的优点  
 RBS 具有以下优点：  
  
### <a name="optimized-database-storage-and-performance"></a>优化的数据库存储和性能  
 在数据库中存储 BLOB 可能会占用大量文件空间和昂贵的服务器资源。 RBS 高效地将 BLOB 传输到您选择的专用存储解决方案，在数据库中存储对 BLOB 的引用。 这样可以释放服务器存储空间用于结构化数据，释放服务器资源用于进行数据库操作。  
  
### <a name="efficient-management-of-blobs"></a>高效管理 BLOB  
 几项 RBS 功能支持对存储的 BLOB 进行方便的管理：  
  
-   BLOB 是通过 ACID（原子性、一致性、隔离性和持久性）事务管理的。  
  
-   BLOB 组织成集合。  
  
-   包括垃圾收集、一致性检查和其他维护功能。  
  
### <a name="standardized-api"></a>标准化 API  
 RBS 定义一组 API，可为应用程序提供用于访问和修改任何 BLOB 存储的标准化编程模型。 每个 BLOB 存储区都可以指定自己的提供程序库，该库嵌入 RBS 客户端库，指定存储和访问 BLOB 的方式。  
  
 许多第三方存储解决方案供应商都开发了符合这些标准 API、在不同存储平台上支持 BLOB 存储的 RBS 提供程序。  
  
## <a name="rbs-requirements"></a>RBS 要求  
 对于存储 BLOB 元数据的主数据库服务器，RBS 要求安装有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise。 但是，如果使用提供的 FILESTREAM 提供程序，则可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard 上存储 BLOB 本身。  
  
 RBS 包括 FILESTREAM 提供程序，因此，您可以使用 RBS 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例上存储 BLOB。 如果要使用 RBS 在其他存储解决方案中存储 BLOB，则必须使用为该存储解决方案开发的第三方 RBS 提供程序，或者使用 RBS API 开发自定义 RBS 提供程序。 [Codeplex](https://go.microsoft.com/fwlink/?LinkId=210190)上以学习资源的形式提供了在 NTFS 文件系统中存储 BLOB 的示例提供程序。  
  
## <a name="rbs-security"></a>RBS 安全性  
 当您使用自定义提供程序在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 外存储 BLOB 时，这些 BLOB 可能会被绕过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全系统的其他进程所利用。 请确保您使用适合于自定义提供程序所使用的存储介质的权限和加密选项保护存储的 BLOB。  
  
##  <a name="rbsresources"></a> RBS 资源  
 **RBS 文档**  
 RBS 文档包括在 Windows 安装程序包中。 如果您想要不安装 RBS 就查看 RBS 文档，则可以在 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] MSDN 库 [中在线查看该文档的](https://go.microsoft.com/fwlink/?LinkId=210192)版本。  
  
 **RBS 白皮书**  
 你可以下载 Microsoft Word 文档格式的白皮书“[远程 BLOB 存储区](https://go.microsoft.com/fwlink/?LinkId=210422)”，它提供有关安装和配置 RBS 的详细信息。  
  
 **RBS 示例**  
 [Codeplex](https://go.microsoft.com/fwlink/?LinkId=210190) 上提供的 RBS 示例演示如何开发 RBS 应用程序，如何开发和安装自定义 RBS 提供程序。  
  
 **RBS 博客**  
 [RBS 博客](https://go.microsoft.com/fwlink/?LinkId=210315) 提供可帮助你理解、部署和维护 RBS 的其他信息。  
  
  
