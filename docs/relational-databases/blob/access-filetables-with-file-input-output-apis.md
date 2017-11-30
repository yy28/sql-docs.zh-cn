---
title: "使用文件输入/输出 API 访问 FileTable | Microsoft Docs"
ms.custom: 
ms.date: 08/25/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: FileTables [SQL Server], accessing files with file APIs
ms.assetid: fa504c5a-f131-4781-9a90-46e6c2de27bb
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6e9485840cba88623f686d33899475f0f572babe
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="access-filetables-with-file-input-output-apis"></a>使用文件输入输出 API 访问 FileTable
  说明如何在 FileTable 上执行文件系统 I/O。  
  
##  <a name="accessing"></a> 开始使用文件 I/O API 访问 FileTable  
 应主要通过 Windows 文件系统和文件 I/O API 来使用 FileTable。 FileTable 通过一组丰富的可用文件 I/O API 支持非事务性访问。  
  
1.  文件 I/O API 访问一般通过获得文件或目录的逻辑 UNC 路径来开始。 应用程序可以将 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句与 [GetFileNamespacePath (Transact-SQL)](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md) 函数结合使用来获取文件或目录的逻辑路径。 有关详细信息，请参阅 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)。  
  
2.  然后，应用程序使用此逻辑路径来获取文件或目录的句柄并对该对象执行操作。 可将此路径传递给任何支持的文件系统 API 函数（如 CreateFile() 或 CreateDirectory()），以创建或打开文件并获取句柄。 然后，该句柄可用于流式传输数据、枚举或组织目录、获取或设置文件属性、删除文件或目录等。  
  
##  <a name="create"></a> 在 FileTable 中创建文件和目录  
 可以通过调用文件 I/O API（如 CreateFile 或 CreateDirectory）在 FileTable 中创建文件或目录。  
  
-   支持所有创建处理标志、共享模式和访问模式。 这包括文件创建、删除和就地修改。 还支持文件命名空间更新，即目录的创建/删除、重命名及移动操作。  
  
-   创建新文件或目录对应于在基础 FileTable 中创建新行。  
  
-   对于文件，流数据存储在 **file_stream** 列中；对于目录，此列为 Null。  
  
-   对于文件， **is_directory** 列包含 **false**。 对于目录，此列包含 **true**。  
  
-   当多个并发文件 I/O 操作或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 操作影响层次结构中的同一个文件或目录时，将强制执行访问共享和并发。  
  
##  <a name="read"></a> 在 FileTable 中读取文件和目录  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中针对流和属性数据的所有文件 I/O 访问操作强制实行“已提交读”隔离语义。  
  
##  <a name="write"></a> 在 FileTable 中写入和更新文件和目录  
  
-   针对 FileTable 的所有文件 I/O 写或更新操作都为非事务性的。 也即，不将任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事务绑定到这些操作，且不提供 ACID 担保。  
  
-   对于 FileTable，支持所有文件 I/O 流式处理/就地更新。  
  
-   通过文件 I/O API 更新 FILESTREAM 数据或属性会导致更新 FileTable 中相应的 **file_stream** 和文件属性列。  
  
##  <a name="delete"></a> 在 FileTable 中删除文件和目录  
 当您删除一个文件或目录时，系统将强制实行所有 Windows 文件 I/O API 语义。  
  
-   如果该目录包含任何文件或子目录，删除目录操作则将失败。  
  
-   删除文件或目录时，将从 FileTable 中删除相应的行。 这与通过 [!INCLUDE[tsql](../../includes/tsql-md.md)] 操作删除行等效。  
  
##  <a name="supported"></a> 支持的文件系统操作  
 FileTable 支持与以下文件系统操作相关的文件系统 API：  
  
-   目录管理  
  
-   文件管理  
  
 FileTable 不支持以下操作：  
  
-   磁盘管理  
  
-   卷管理  
  
-   事务性 NTFS  
  
##  <a name="considerations"></a> 使用文件 I/O 访问 FileTable 的其他注意事项  
  
###  <a name="vnn"></a> 将虚拟网络名称 (VNN) 用于 AlwaysOn 可用性组  
 在包含 FILESTREAM 或 FileTable 数据的数据库属于某一 AlwaysOn 可用性组时，通过文件系统 API 对 FILESTREAM 或 FileTable 数据进行的所有访问都应该使用 VNN，而非计算机名称。 有关详细信息，请参阅 [FILESTREAM 和 FileTable 与 AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md)。  
  
###  <a name="partial"></a> 部分更新  
 使用 [GetFileNamespacePath (Transact-SQL)](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md) 函数为 FileTable 中的 FILESTREAM 数据获取的可写句柄可用于对 FILESTREAM 内容执行就地部分更新。 此行为不同于通过调用 **OpenSQLFILESTREAM()** 并传递显式事务上下文所获取的手柄进行事务性 FILESTREAM 访问。  
  
###  <a name="trans"></a> 事务性语义  
 当使用文件 I/O API 访问 FileTable 中的文件时，这些操作不与任何用户事务关联，并且具有以下其他特性：  
  
-   由于对 FileTable 中 FILESTREAM 数据的非事务性访问不与任何事务关联，因此它不具有任何特定的隔离语义。 但是， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以使用内部事务来对 FileTable 数据强制执行锁定或并发语义。 这种类型的任何内部事务都采用“已提交读”隔离模式来执行。  
  
-   对于 FILESTREAM 数据的这些非事务性操作，没有 ACID 担保。 一致性担保类似于应用程序在文件系统中进行文件更新时的担保。  
  
-   不能回滚这些更改。  
  
 但是，也可以通过调用 **OpenSqlFileStream()**，借助事务性 FILESTREAM 访问来访问 FileTable 中的 FILESTREAM 列。 这种访问可以是纯事务性的，将具有当前支持的所有事务性一致性级别。  
  
###  <a name="concurrency"></a> 并发控制  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 为文件系统应用程序间以及在文件系统应用程序与 [!INCLUDE[tsql](../../includes/tsql-md.md)] 应用程序间的 FileTable 访问强制执行并发控制。 通过持有 FileTable 行的相应锁来实现此并发控制。  
  
###  <a name="triggers"></a> 触发器  
 通过文件系统创建、修改或删除文件或目录或其属性，将导致在 FileTable 中进行相应的插入、更新或删除操作。 任何关联的 [!INCLUDE[tsql](../../includes/tsql-md.md)] DML 触发器都将作为这些操作的一部分激发。  
  
##  <a name="funclist"></a> FileTable 中支持的文件系统功能  
  
|功能|Supported|注释|  
|----------------|---------------|--------------|  
|**Oplocks**|是|支持级别 2、级别 1、批处理和筛选器 oplocks。|  
|**扩展属性**|是||  
|**重分析点**|是||  
|**持久的 ACL**|是||  
|**命名的流**|是||  
|**稀疏文件**|是|只能对文件设置稀疏性，它影响数据流的存储方式。 由于 FILESTREAM 数据存储在 NTFS 卷上，因此 FileTable 功能支持通过将请求转发给 NTFS 文件系统来支持稀疏文件。|  
|**压缩**|是||  
|**加密**|是||  
|**TxF**|是||  
|**文件 ID**|是||  
|**对象 ID**|是||  
|**符号链接**|是||  
|**硬链接**|是||  
|**短名称**|是||  
|**目录更改通知**|是||  
|**字节范围锁定**|是|将对字节范围的锁定请求传递给 NTFS 文件系统。|  
|**内存映射文件**|是||  
|**取消 I/O**|是||  
|**安全性**|是|实施 Windows 共享级安全性和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表以及列级安全性。|  
|**USN 日志**|是|对 FileTable 中的文件和目录的元数据更改是对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的 DML 操作。 因此，将它们记录在相应的数据库日志文件中。 但是，不将它们记录在 NTFS USN 日志（对大小的更改除外）中。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更改跟踪功能可用于捕获类似的信息。|  
  
## <a name="see-also"></a>另请参阅  
 [将文件加载到 FileTable 中](../../relational-databases/blob/load-files-into-filetables.md)   
 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)   
 [使用 Transact-SQL 访问 FileTable](../../relational-databases/blob/access-filetables-with-transact-sql.md)   
 [FileTable DDL、函数、存储过程和视图](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
  
  
