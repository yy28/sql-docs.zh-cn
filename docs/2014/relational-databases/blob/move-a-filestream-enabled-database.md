---
title: 移动启用了 FILESTREAM 的数据库 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: filestream
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], moving a FILESTREAM-enabled database
ms.assetid: dd4d270d-9283-431a-aa6b-e571fced1893
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cf263ca51d07319acb0b3284191a787cac44b734
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37316557"
---
# <a name="move-a-filestream-enabled-database"></a>移动启用了 FILESTREAM 的数据库
  本主题演示如何移动启用了 FILESTREAM 的数据库。  
  
> [!NOTE]  
>  本主题中的示例需要使用在 [创建启用了 FILESTREAM 的数据库](create-a-filestream-enabled-database.md)中创建的存档数据库。  
  
### <a name="to-move-a-filestream-enabled-database"></a>移动启用了 FILESTREAM 的数据库  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，单击 **“新建查询”** 以打开查询编辑器。  
  
2.  将以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本复制到查询编辑器中，然后单击“执行”。  此脚本显示 FILESTREAM 数据库所使用的物理数据库文件的位置。  
  
    ```tsql  
    USE Archive  
    GO  
    SELECT type_desc, name, physical_name from sys.database_files  
    ```  
  
3.  将以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本复制到查询编辑器中，然后单击“执行”。  此代码使 `Archive` 数据库脱机。  
  
    ```tsql  
    USE master  
    EXEC sp_detach_db Archive  
    GO  
    ```  
  
4.  创建文件夹 `C:\moved_location`，然后将步骤 2 中列出的文件和文件夹移动到该文件夹中。  
  
5.  将以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本复制到查询编辑器中，然后单击“执行”。  此脚本将 `Archive` 数据库设置为脱机。  
  
    ```tsql  
    CREATE DATABASE Archive ON  
    PRIMARY ( NAME = Arch1,  
        FILENAME = 'c:\moved_location\archdat1.mdf'),  
    FILEGROUP FileStreamGroup1 CONTAINS FILESTREAM( NAME = Arch3,  
        FILENAME = 'c:\moved_location\filestream1')  
    LOG ON  ( NAME = Archlog1,  
        FILENAME = 'c:\moved_location\archlog1.ldf')  
    FOR ATTACH  
    GO  
    ```  
  
## <a name="see-also"></a>请参阅  
 [sp_detach_db (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-detach-db-transact-sql)  
  
  
