---
title: 创建表以存储 FILESTREAM 数据 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], table storage
ms.assetid: 029c3059-5c83-43e2-a859-9027031b7de1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3846c714c0b1bcc1f8953a553f1c5b177503919b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65094245"
---
# <a name="create-a-table-for-storing-filestream-data"></a>创建表以存储 FILESTREAM 数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题说明如何创建表以存储 FILESTREAM 数据。  
  
 如果数据库具有 FILESTREAM 文件组，则可以创建或修改表以存储 FILESTREAM 数据。 若要指定某个列包含 FILESTREAM 数据，请创建一个 **varbinary(max)** 列并添加 FILESTREAM 属性。  
  
### <a name="to-create-a-table-to-store-filestream-data"></a>创建表以存储 FILESTREAM 数据  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，单击“新建查询”  以显示查询编辑器。  
  
2.  将下面示例的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码复制到查询编辑器中。 此 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码可创建一个启用了 FILESTREAM 的表，称为 Records。  
  
3.  若要创建该表，请单击 **“执行”** 。  
  
## <a name="example"></a>示例  
 下面的代码示例说明了如何创建一个名为 `Records`的表。 `Id` 列是一个 `ROWGUIDCOL` 列，通过 Win32 API 使用 FILESTREAM 数据时需要使用该列。 `SerialNumber` 列是一个 `UNIQUE INTEGER`列。 `Chart` 列是一个 `FILESTREAM` 列，用于在文件系统中存储 `Chart` 。  
  
> [!NOTE]  
>  本示例是在 [创建启用了 FILESTREAM 的数据库](../../relational-databases/blob/create-a-filestream-enabled-database.md)中创建的 Archive 数据库。  
  
 [!code-sql[FILESTREAM#FS_CreateTable](../../relational-databases/blob/codesnippet/tsql/create-a-table-for-stori_1.sql)]  
  
## <a name="see-also"></a>另请参阅  
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
