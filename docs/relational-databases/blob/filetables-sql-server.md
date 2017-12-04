---
title: FileTable (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 10/24/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: blob
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FileTables [SQL Server], overview
- FileTables [SQL Server]
- FileTable [SQL Server], see FileTables [SQL Server]
- FileTable [SQL Server]
ms.assetid: a57b629c-e9ed-48fd-9a48-ed3787d80c8f
caps.latest.revision: "20"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: d8d5ce9a3a0ab49fb62fd434fe523ecfa937c6ad
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="filetables-sql-server"></a>FileTable (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]FileTable 功能为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中存储的文件数据提供对 Windows 文件命名空间的支持以及与 Windows 应用程序的兼容性支持。 FileTable 使得应用程序可以集成其存储和数据管理组件，可对非结构化数据和元数据提供集成的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务（包括全文搜索和语义搜索）。  
  
 换言之，您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中将文件和文档存储在称作 FileTable 的特别的表中，但是从 Windows 应用程序访问它们，就好像它们存储在文件系统中，而不必对您的客户端应用程序进行任何更改。  
  
 FileTable 功能是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] FILESTREAM 技术的基础上生成的。 有关 FILESTREAM 的详细信息，请参阅 [FILESTREAM (SQL Server)](../../relational-databases/blob/filestream-sql-server.md)。  
  
##  <a name="Goals"></a> FileTable 功能的优点  
 FileTable 功能的目标包括：  
  
-   针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中存储的文件数据的 Windows API 兼容性。 Windows API 兼容性包括以下方面：  
  
    -   对 FILESTREAM 数据的非事务性流式访问和就地更新。  
  
    -   目录和文件的分层命名空间。  
  
    -   文件属性的存储，如创建日期和修改日期。  
  
    -   对 Windows 文件和目录管理 API 的支持。  
  
-   与其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能的兼容性包括针对 FILESTREAM 和文件属性数据的管理工具、服务和关系查询功能。  
  
 这样，FileTable 将消除使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 来存储和管理非结构化数据的一个巨大障碍，这些数据目前作为文件存储在文件服务器上。 企业可以将这些数据从文件服务器移到 FileTable，以利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供的集成管理和服务。 同时，它们可以保持现有 Windows 应用程序的 Windows 应用程序兼容性，将这些数据视为文件系统中的文件。  
 
  
##  <a name="Description"></a> 什么是 FileTable？  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对于需要在数据库中存储文件和目录的应用程序，借助 Windows API 兼容性和非事务性访问，提供一种特殊的 **文件表**，也称为 **FileTable**。 FileTable 是一种专用的用户表，它包含存储 FILESTREAM 数据的预定义架构以及文件和目录层次结构信息、文件属性。  
  
 FileTable 提供以下功能：  
  
-   FileTable 表示目录和文件的一种层次结构。 它为目录和其中所含的文件存储与该层次结构中所有节点有关的数据。 该层次结构以您创建 FileTable 时指定的根目录为起点。  
  
-   FileTable 中的每行表示一个文件或目录。  
  
-   每行包含以下项： 有关 FileTable 的架构的详细信息，请参阅 [FileTable Schema](../../relational-databases/blob/filetable-schema.md)。  
  
    -   流数据的 file_stream 列和 stream_id (GUID) 标识符。 （ **file_stream** 列对于目录为 NULL。）  
  
    -   用于表示和维护当前项（文件或目录）以及目录层次结构的 path_locator 列和 parent_path_locator 列。  
  
    -   10 个文件属性，如可用于文件 I/O API 的创建日期和修改日期。  
  
    -   支持针对文件和文档的全文搜索和语义搜索的类型列。  
  
-   FileTable 强制执行某些系统定义的约束和触发器以维护文件命名空间语义。  
  
-   针对非事务性访问配置数据库时，在为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例配置的 FILESTREAM 共享区下公开在 FileTable 中表示的文件和目录层次结构。 这为 Windows 应用程序提供了文件系统访问方法。  
  
 FileTable 的一些其他特性包括：  
  
-   存储在 FileTable 中的文件和目录数据通过用于非事务性文件访问的 Windows 共享区（针对基于 Windows API 的应用程序）公开。 对于 Windows 应用程序，这看起来像一个包含文件和目录的普通共享区。 应用程序可使用一组广泛的 Windows API，用于对此共享区下的文件和目录进行管理。  
  
-   通过该共享区公开的目录层次结构是一个在 FileTable 中维护的纯逻辑目录结构。  
  
-   通过该 Windows 共享区对创建或更改文件/目录的调用被 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件拦截并在 FileTable 中的相应关系数据中得到反映。  
  
-   Windows API 操作本质上是非事务性的，并不与用户事务关联。 但是，完全支持对存储在 FileTable 中的 FILESTREAM 数据的事务性访问，就像对待常规表中的任何 FILESTREAM 列一样。  
  
-   还可以通过常规 [!INCLUDE[tsql](../../includes/tsql-md.md)] 访问来查询和更新 FileTable。 它们还与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理工具和诸如备份的功能集成。  
  
##  <a name="additional"></a> 使用 FileTable 的其他注意事项  
  
###  <a name="DBA"></a> 管理注意事项  
 **关于 FILESTREAM 和 FileTable**  
  
-   独立于 FILESTREAM 配置 FileTable。 因此，您可以继续使用 FILESTREAM 功能，而不启用非事务性访问或创建 FileTable。  
  
-   除了通过 FileTable，没有对 FILESTREAM 数据的其他非事务性访问。 因此，在启用非事务性访问时并不会影响现有的 FILESTREAM 列和应用程序的行为。  
  
 **关于 FileTable 和非事务性访问**  
  
-   可以在数据库级别启用或禁用非事务性访问。  
  
-   您可以通过将非事务性访问关闭或者启用只读或完全读/写访问，在数据库级别配置或优化非事务性访问。  
   
###  <a name="memory"></a> FileTable 不支持内存映射文件  
 FileTable 不支持内存映射文件。 “记事本”和“画图”是两个常见的使用内存映射文件的示例应用程序。 不能在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所在的计算机上使用这些应用程序来打开存储在 FileTable 中的文件。 但是，可以从远程计算机使用这些应用程序来打开存储在 FileTable 中的文件，因为在这些情况下不使用内存映射功能。  
   
##  <a name="reltasks"></a> 相关任务  
 [启用 FileTable 的先决条件](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)  
 介绍如何启用创建和使用 FileTable 的先决条件。  
  
 [创建、更改和删除 FileTable](../../relational-databases/blob/create-alter-and-drop-filetables.md)  
 说明如何创建新的 FileTable 或者更改或删除现有的 FileTable。  
  
 [将文件加载到 FileTable 中](../../relational-databases/blob/load-files-into-filetables.md)  
 说明如何将文件加载或迁移到 FileTable 中。  
  
 [在 FileTable 中使用目录和路径](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
 说明 FileTable 中用于存储文件的目录结构。  
  
 [使用 Transact-SQL 访问 FileTable](../../relational-databases/blob/access-filetables-with-transact-sql.md)  
 说明 Transact-SQL 数据操作语言 (DML) 命令如何与 FileTable 一起使用。  
  
 [使用文件输入输出 API 访问 FileTable](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)  
 说明如何在 FileTable 上执行文件系统 I/O。  
  
 [管理 FileTable](../../relational-databases/blob/manage-filetables.md)  
 说明用于管理 FileTable 的常见管理任务。  
  
##  <a name="relcontent"></a> 相关内容  
 [FileTable Schema](../../relational-databases/blob/filetable-schema.md)  
 说明 FileTable 的预定义固定架构。  
  
 [FileTable 与其他 SQL Server 功能的兼容性](../../relational-databases/blob/filetable-compatibility-with-other-sql-server-features.md)  
 说明 FileTable 如何与 SQL Server 的其他功能配合使用。  
  
 [FileTable DDL、函数、存储过程和视图](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
 列出用于支持 FileTable 功能的新增或更改的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库对象。  
  
  
