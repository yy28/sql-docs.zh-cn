---
title: MSSQLSERVER_3181 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3181 (Database Engine error)
ms.assetid: e6d2e716-5263-477c-ad0e-7bcbfef4c1f3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a9f7332460d3dc25c756e6bd031b1a4b3a1f6743
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62868762"
---
# <a name="mssqlserver3181"></a>MSSQLSERVER_3181
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|3181|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|LDDB_STORAGE_VERIFY|  
|消息正文|还原此备份的尝试可能会遇到存储空间问题。 后续消息将提供详细信息。|  
  
## <a name="explanation"></a>解释  
 RESTORE VERIFYONLY 语句会检查数据库将还原到的磁盘上的可用存储空间。  
  
### <a name="possible-causes"></a>可能的原因  
 可用磁盘空间不足，因此无法还原要验证的备份。  
  
## <a name="user-action"></a>用户操作  
 将备份还原到拥有足够磁盘空间的位置，或提供更多磁盘空间。  
  
## <a name="see-also"></a>请参阅  
 [将数据库还原到新位置 (SQL Server)](../backup-restore/restore-a-database-to-a-new-location-sql-server.md)   
 [文件还原到新位置&#40;SQL Server&#41;](../backup-restore/restore-files-to-a-new-location-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [RESTORE VERIFYONLY (Transact-SQL)](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql)  
  
  
