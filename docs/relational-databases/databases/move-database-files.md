---
title: 移动数据库文件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], moving database files
- files [SQL Server], moving
- data files [SQL Server], moving
- file moving [SQL Server]
- moving full-text catalogs
- moving databases
- full-text catalogs [SQL Server], moving
- moving database files
- scheduled disk maintenance [SQL Server]
- moving files
- relocating database files
- planned database relocations [SQL Server]
- databases [SQL Server], moving
ms.assetid: 89f01b10-5fae-4ed8-b0fb-a4b9f540fd28
author: stevestein
ms.author: sstein
ms.openlocfilehash: c53e9ee51714ebfcce81a722f78a4f79cbc2530f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "68067318"
---
# <a name="move-database-files"></a>移动数据库文件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，可以通过在 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 语句的 FILENAME 子句中指定新的文件位置来移动系统数据库和用户数据库。 数据、日志和全文目录文件也可以通过此方法进行移动。 这在下列情况下可能很有用：  
  
-   故障恢复。 例如，由于硬件故障，数据库处于可疑模式或被关闭。  
  
-   预先安排的重定位。  
  
-   为预定的磁盘维护操作而进行的重定位。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|说明|  
|-----------|-----------------|  
|[移动用户数据库](../../relational-databases/databases/move-user-databases.md)|说明将用户数据库文件和全文目录文件移动到新位置的过程。|  
|[移动系统数据库](../../relational-databases/databases/move-system-databases.md)|说明将系统数据库文件移动到新位置的过程。|  
  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [数据库分离和附加 (SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  
