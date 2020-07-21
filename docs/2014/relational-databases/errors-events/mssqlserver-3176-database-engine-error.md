---
title: MSSQLSERVER_3176 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3176 (Database Engine error)
ms.assetid: 4be24c64-2d52-4cb4-b4d7-36efbe4555b6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6e23d62f8d0b24595ef16d07a3ffb973c9c449ec
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551772"
---
# <a name="mssqlserver_3176"></a>MSSQLSERVER_3176
    
## <a name="details"></a>详细信息  
  
|Attribute|值|  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|3176|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|LDDB_FILE_CLAIM|  
|消息正文|'%ls'(%d)和 '%ls'(%d)要求使用文件 '%ls'。 WITH MOVE 子句可用于重新定位一个或多个文件。|  
  
## <a name="explanation"></a>说明  
 尝试在多项操作中使用同一文件。  
  
### <a name="possible-causes"></a>可能的原因  
 其他数据库已经在使用该文件名。  
  
## <a name="user-action"></a>用户操作  
 将数据库文件还原到不同位置。 在 RESTORE 语句中，使用 WITH MOVE 子句移动各个文件。 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，在“还原数据库选项”对话框的“将数据库文件还原为”网格中更改文件位置。  
  
## <a name="see-also"></a>另请参阅  
 [将数据库还原到新位置 (SQL Server)](../backup-restore/restore-a-database-to-a-new-location-sql-server.md)   
 [将文件还原到 &#40;SQL Server 的新位置&#41;](../backup-restore/restore-files-to-a-new-location-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
