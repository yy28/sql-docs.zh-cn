---
title: 使用 Transact-SQL 访问 FileTable | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], accessing files with T-SQL
ms.assetid: 3c4a5ffb-c521-4696-99cb-2b03cffc9c02
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c86ab8b3f29699e807c61b571832c106ab235710
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018889"
---
# <a name="access-filetables-with-transact-sql"></a>使用 Transact-SQL 访问 FileTable
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  说明 [!INCLUDE[tsql](../../includes/tsql-md.md)] 数据操作语言 (DML) 命令如何与 FileTable 一起使用。  
  
##  <a name="BasicsInsert"></a> FileTable 上的 INSERT 操作  
 下列注意事项适用于 FileTable 上的 **INSERT** 操作：  
  
-   所有文件属性列具有 NOT NULL 约束。 如果没有显式设置值，则提供适当的默认值。  
  
-   如果 INSERT 语句设置了 **name**、**path_locator**、**parent_path_locator** 或文件属性，则强制执行系统定义的约束。  
  
-   该应用程序可以通过提供指向 [GetPathLocator (Transact-SQL)](../../relational-databases/system-functions/getpathlocator-transact-sql.md) 函数的文件系统路径，来获取文件或目录的 **path_locator**。  
  
##  <a name="BasicsUpdate"></a> FileTable 上的 UPDATE 操作  
 下列注意事项适用于 FileTable 上的 **UPDATE** 操作：  
  
-   允许更新任何用户定义的数据。  
  
-   如果 INSERT 语句设置了 **name**、 **path_locator**、 **parent_path_locator**或文件属性，则强制执行系统定义的约束。  
  
-   可以对 **file_stream** 列中的 FILESTREAM 数据进行更新，且不会影响任何其他列（包括时间戳）。  
  
##  <a name="BasicsDelete"></a> FileTable 上的 DELETE 操作  
 下列注意事项适用于 FileTable 上的 **DELETE** 操作：  
  
-   删除行还将从文件系统中删除相应的文件或目录。  
  
-   如果该行与包含其他文件或目录的目录相对应，则删除行操作将失败。  
  
##  <a name="BasicsConstraints"></a> 针对 FileTable 的 DML 操作强制执行的约束  
 系统定义的约束确保 DML 操作不破坏文件命名空间层次结构的完整性。 强制执行的约束包括：  
  
-   当您设置或更改文件或目录的 **名称** 时：  
  
    -   将强制执行 Windows 文件或目录命名约定。  
  
    -   将强制实施父目录中名称的唯一性。  
  
-   当通过设置或更改 **path_locator** 或 **parent_path_locator**来设置或更改文件或目录的位置时：  
  
    -   强制执行唯一性。  
  
    -   将强制执行目录和文件的层次结构树的一致性，包括 **path_locator** 和 **parent_path_locator** 值的一致性。  
  
-   当 **file_stream** 列为非 Null 时，不能将 **is_directory** 的值设置为 True。 **file_stream** 列中的数据指示该行表示一个文件，而不是一个目录。  
  
-   文件属性列不能为 Null。 将使用默认值强制执行 NOT NULL 约束。  
  
-   **last_access_time** 的值不能早于 **last_write_time** 和 **creation_time**。  
  
## <a name="see-also"></a>另请参阅  
 [将文件加载到 FileTable 中](../../relational-databases/blob/load-files-into-filetables.md)   
 [在 FileTable 中使用目录和路径](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)   
 [使用文件输入输出 API 访问 FileTable](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)   
 [FileTable DDL、函数、存储过程和视图](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
  
  
