---
title: 在 FileTable 中使用目录和路径 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], directories
ms.assetid: f1e45900-bea0-4f6f-924e-c11e1f98ab62
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 321c452c816f765642d14142a64ab88f5ecb9cdf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198787"
---
# <a name="work-with-directories-and-paths-in-filetables"></a>在 FileTable 中使用目录和路径
  说明 FileTable 中用于存储文件的目录结构。  
  
##  <a name="HowToDirectories"></a> 如何在 FileTable 中使用目录和路径  
 您可以使用以下 3 个函数以便在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中使用 FileTable 目录：  
  
|为得到这一结果|使用此函数|  
|------------------------|-----------------------|  
|获取特定 FileTable 或当前数据库的根级 UNC 路径。|[FileTableRootPath (Transact-SQL)](/sql/relational-databases/system-functions/filetablerootpath-transact-sql)|  
|获取 FileTable 中文件或目录的绝对或相对 UNC 路径。|[GetFileNamespacePath (Transact-SQL)](/sql/relational-databases/system-functions/getfilenamespacepath-transact-sql)|  
|通过提供路径，获取 FileTable 中指定文件或目录的路径定位器 ID 值。|[GetPathLocator (Transact-SQL)](/sql/relational-databases/system-functions/getpathlocator-transact-sql)|  
  
##  <a name="BestPracticeRelativePaths"></a> 如何使用相对路径编写可移植代码  
 若要使代码和应用程序独立于当前的计算机和数据库，应避免编写依赖于绝对文件路径的代码。 可通过使用 [FileTableRootPath (Transact SQL )](/sql/relational-databases/system-functions/filetablerootpath-transact-sql) 和 [GetFileNamespacePath (Transact-SQL)](/sql/relational-databases/system-functions/getfilenamespacepath-transact-sql) 函数组合在运行时获取文件的完整路径，如下例所示。 默认情况下，`GetFileNamespacePath` 函数返回数据库根路径下的文件的相对路径。  
  
```tsql  
USE database_name;  
DECLARE @root nvarchar(100);  
DECLARE @fullpath nvarchar(1000);  
  
SELECT @root = FileTableRootPath();  
SELECT @fullpath = @root + file_stream.GetFileNamespacePath()  
    FROM filetable_name  
    WHERE name = N'document_name';  
  
PRINT @fullpath;  
GO  
```  
  
##  <a name="restrictions"></a> 重要限制  
  
###  <a name="nesting"></a> 嵌套级别  
  
> [!IMPORTANT]  
>  您不能在 FileTable 目录中存储超过 15 个级别的子目录。 在您存储 15 个级别的子目录时，最下面的一级不能包含文件，因为这些文件将代表另外一个级别。  
  
###  <a name="fqnlength"></a> 完整路径名的长度  
  
> [!IMPORTANT]  
>  NTFS 文件系统支持远远超过 Windows 外壳程序和大多数 Windows API 的 260 个字符限制的路径名。 因此，使用 Transact-SQL 在 FileTable 的文件层次结构中创建的文件有可能无法使用 Windows 资源管理器或很多其他 Windows 应用程序查看或打开，原因是这些文件的完整路径名称超过了 260 个字符。 但是，您可使用 Transact-SQL 继续访问这些文件。  
  
##  <a name="fullpath"></a> FileTable 中存储的项的完整路径  
 FileTable 中存储的文件或目录的完整路径用以下元素开头：  
  
1.  为在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例级别进行 FILESTREAM 文件 I/O 访问启用的共享区。  
  
2.  在数据库级别指定的 **DIRECTORY_NAME** 。  
  
3.  在 FileTable 级别指定的 **FILETABLE_DIRECTORY** 。  
  
 生成的层次结构如下所示：  
  
 `\\<machine>\<instance-level FILESTREAM share>\<database-level directory>\<FileTable directory>\`  
  
 此目录层次结构构成了 FileTable 的文件命名空间的根。 在此目录层次结构下，FileTable 的 FILESTREAM 数据作为文件存储，并且存储为也包含文件和子目录的子目录。  
  
 请务必记住，在此实例级别 FILESTREAM 共享区下创建的目录层次结构是虚拟目录层次结构。 该层次结构存储于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中，并且在物理上不在 NTFS 文件系统中表示。 访问 FILESTREAM 共享区之下和其包含的 FileTable 中的文件和目录的所有操作都将被文件系统中嵌入的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件拦截和处理。  
  
##  <a name="roots"></a> 实例级、数据库级和 FileTable 级根目录的语义  
 此目录层次结构遵循下面的语义：  
  
-   实例级别 FILESTREAM 共享区由管理员配置并且存储为服务器的属性。 您可以通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器，重命名该存储区。 在重新启动服务器之前，重命名操作将不会生效。  
  
-   在创建新的数据库时，数据库级别 **DIRECTORY_NAME** 默认为 Null。 管理员可以通过使用 **ALTER DATABASE** 语句设置或更改此名称。 此名称在该实例中必须唯一（不区分大小写比较时）。  
  
-   在创建 FileTable 时，通常提供 **FILETABLE_DIRECTORY** 名称作为 **CREATE TABLE** 语句的一部分。 您可以通过使用 **ALTER TABLE** 命令来更改此名称。  
  
-   不能通过文件 I/O 操作来重命名这些根目录。  
  
-   不能使用独占式文件句柄打开这些根目录。  
  
##  <a name="is_directory"></a> FileTable 架构中的 is_directory 列  
 下表说明 **is_directory** 列与包含 FileTable 中 FILESTREAM 数据的 **file_stream** 列之间的相互影响：  
  
||||  
|-|-|-|  
|*is_directory* **值**|*file_stream* **值**|**行为**|  
|FALSE|NULL|这是将被系统定义的约束捕获的无效组合。|  
|FALSE|\<value>|该项表示一个文件。|  
|TRUE|NULL|该项表示一个目录。|  
|TRUE|\<value>|这是将被系统定义的约束捕获的无效组合。|  
  
##  <a name="alwayson"></a> 将虚拟网络名称 (VNN) 用于 AlwaysOn 可用性组  
 在包含 FILESTREAM 或 FileTable 数据的数据库属于某一 AlwaysOn 可用性组时：  
  
-   FILESTREAM 和 FileTable 函数接受或返回虚拟网络名称 (VNN)，而非计算机名称。 有关这些函数的详细信息，请参阅 [Filestream 和 FileTable 函数 (Transact-SQL)](/sql/relational-databases/system-functions/filestream-and-filetable-functions-transact-sql)。  
  
-   通过文件系统 API 对 FILESTREAM 或 FileTable 数据进行的所有访问都应该使用 VNN，而非计算机名称。 有关详细信息，请参阅 [FILESTREAM 和 FileTable 与 AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md)。  
  
## <a name="see-also"></a>请参阅  
 [启用 FileTable 的先决条件](enable-the-prerequisites-for-filetable.md)   
 [创建、更改和删除 FileTable](create-alter-and-drop-filetables.md)   
 [使用 Transact-SQL 访问 FileTable](access-filetables-with-transact-sql.md)   
 [使用文件输入输出 API 访问 FileTable](access-filetables-with-file-input-output-apis.md)  
  
  
