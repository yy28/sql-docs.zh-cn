---
title: 创建启用了 FILESTREAM 的数据库 | Microsoft Docs
description: 创建或更改数据库时，使用 CONTAINS FILESTREAM 子句配置数据库以支持 FILESTREAM。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], FILESTREAM-enabled databases
ms.assetid: 0fc16356-76f7-44b8-a58b-f0b7c43694ec
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ad66d6d5b6aa32ba8f2e594dbba91c07940d185a
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809963"
---
# <a name="create-a-filestream-enabled-database"></a>创建启用了 FILESTREAM 的数据库
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  本主题说明如何创建支持 FILESTREAM 的数据库。 由于 FILESTREAM 使用一种特殊类型的文件组，因此，在创建数据库时，必须至少为一个文件组指定 CONTAINS FILESTREAM 子句。  
  
 一个 FILESTREAM 文件组可以包含多个文件。 有关演示如何创建包含多个文件的 FILESTREAM 文件组的代码示例，请参阅 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-transact-sql.md)。  
  
### <a name="to-create-a-filestream-enabled-database"></a>创建启用了 FILESTREAM 的数据库  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，单击 **“新建查询”** 以显示查询编辑器。  
  
2.  将下面示例的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码复制到查询编辑器中。 此 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码可创建一个启用了 FILESTREAM 的数据库，称为 Archive。  
  
    > [!NOTE]  
    >  对于此脚本，C:\Data 目录必须存在。  
  
3.  若要生成数据库，请单击 **“执行”** 。  

## <a name="example"></a>示例  
 下面的代码示例创建一个名为 `Archive`的数据库。 该数据库包含三个文件组： `PRIMARY`、 `Arch1`和 `FileStreamGroup1`。 `PRIMARY` 和 `Arch1` 是不能包含 FILESTREAM 数据的常规文件组。 `FileStreamGroup1` 是 `FILESTREAM` 文件组。  
  
 [!code-sql[FILESTREAM#FS_CreateDB](../../relational-databases/blob/codesnippet/tsql/create-a-filestream-enab_1.sql)]  
  
 对于 `FILESTREAM` 文件组， `FILENAME` 引用一个路径。 在最后一个文件夹之前的路径必须存在，但不能存在最后一个文件夹。 在此示例中， `c:\data` 必须存在。 但是，在执行 `filestream1` 语句时， `CREATE DATABASE` 子文件夹不能存在。 有关语法的详细信息，请参阅 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-transact-sql.md)。  
  
 在运行上面的示例后，filestream.hdr 文件和 $FSLOG 文件夹将出现在 c:\Data\filestream1 文件夹中。 filestream.hdr 文件是 FILESTREAM 容器的头文件。  
  
> [!IMPORTANT]  
>  filestream.hdr 文件是重要的系统文件。 它包含 FILESTREAM 标头信息。 请勿删除或修改此文件。  
  
 对于现有数据库，可以使用 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 语句来添加 FILESTREAM 文件组。  
  
## <a name="see-also"></a>另请参阅  
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-transact-sql.md)   
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)  
  
