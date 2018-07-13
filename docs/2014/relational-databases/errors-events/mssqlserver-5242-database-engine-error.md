---
title: MSSQLSERVER_5242 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 5242 (Database Engine error)
ms.assetid: 712b1a10-2f87-41df-a111-1ed9f14102d4
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1f9716d57be9d9c287099743fa2c0205174af0b1
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37425366"
---
# <a name="mssqlserver5242"></a>MSSQLSERVER_5242
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|5242|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称||  
|消息正文|在数据库 '%.*ls'(ID:%d) 中对页 %S_PGID 执行内部操作期间检测到不一致性。 请与技术支持联系。 参考号为 %ld。|  
  
## <a name="explanation"></a>解释  
 在错误消息中引用的数据库页上出现结构不一致性。  
  
## <a name="see-also"></a>请参阅  
 [DBCC CHECKDB (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)   
 [数据库文件和文件组](../databases/database-files-and-filegroups.md)  
  
  
