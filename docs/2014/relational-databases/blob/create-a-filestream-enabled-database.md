---
title: 创建启用了 FILESTREAM 的数据库 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], FILESTREAM-enabled databases
ms.assetid: 0fc16356-76f7-44b8-a58b-f0b7c43694ec
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 65de151b2ea2bb59330bae0fa94c9e15d67e4a47
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533539"
---
# <a name="create-a-filestream-enabled-database"></a>创建启用了 FILESTREAM 的数据库
  本主题说明如何创建支持 FILESTREAM 的数据库。 由于 FILESTREAM 使用一种特殊类型的文件组，因此，在创建数据库时，必须至少为一个文件组指定 CONTAINS FILESTREAM 子句。  
  
 一个 FILESTREAM 文件组可以包含多个文件。 有关演示如何创建包含多个文件的 FILESTREAM 文件组的代码示例，请参阅 [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql)。  
  
### <a name="to-create-a-filestream-enabled-database"></a>创建启用了 FILESTREAM 的数据库  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，单击 **“新建查询”** 以显示查询编辑器。  
  
2.  复制[!INCLUDE[tsql](../../includes/tsql-md.md)]代码将创建名为存档的启用了 FILESTREAM 的数据库。  
  
    > [!NOTE]  
    >  对于此脚本，C:\Data 目录必须存在。  
  
3.  若要生成数据库，请单击 **“执行”**。  
  
## <a name="example"></a>示例  
 下面的代码示例创建一个名为 `Archive`的数据库。 该数据库包含三个文件组： `PRIMARY`、 `Arch1`和 `FileStreamGroup1`。 `PRIMARY` 和 `Arch1` 是不能包含 FILESTREAM 数据的常规文件组。 `FileStreamGroup1` 是 `FILESTREAM` 文件组。  
  
```sql  
CREATE DATABASE Archive   
ON  
PRIMARY ( NAME = Arch1,  
    FILENAME = 'c:\data\archdat1.mdf'),  
FILEGROUP FileStreamGroup1 CONTAINS FILESTREAM( NAME = Arch3,  
    FILENAME = 'c:\data\filestream1')  
LOG ON  ( NAME = Archlog1,  
    FILENAME = 'c:\data\archlog1.ldf')  
GO  
```  
  
 对于 `FILESTREAM` 文件组， `FILENAME` 引用一个路径。 在最后一个文件夹之前的路径必须存在，但不能存在最后一个文件夹。 在此示例中， `c:\data` 必须存在。 但是，在执行 `filestream1` 语句时， `CREATE DATABASE` 子文件夹不能存在。 有关语法的详细信息，请参阅 [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql)。  
  
 在运行上面的示例后，filestream.hdr 文件和 $FSLOG 文件夹将出现在 c:\Data\filestream1 文件夹中。 filestream.hdr 文件是 FILESTREAM 容器的头文件。  
  
> [!IMPORTANT]  
>  filestream.hdr 文件是重要的系统文件。 它包含 FILESTREAM 标头信息。 请勿删除或修改此文件。  
  
 对于现有数据库，可以使用 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) 语句来添加 FILESTREAM 文件组。  
  
## <a name="see-also"></a>请参阅  
 [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)  
  
  
