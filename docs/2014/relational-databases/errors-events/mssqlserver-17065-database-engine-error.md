---
title: MSSQLSERVER_17065 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17065 (Database Engine error)
ms.assetid: 63c2ba5a-be34-461e-bee1-03c25b396cd2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 47aebfa29b60a1c2ae50c6699946312996d26e6f
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967917"
---
# <a name="mssqlserver_17065"></a>MSSQLSERVER_17065
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|17065|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLASSERT_BOTH|  
|消息正文|SQL Server 断言：文件： \<%s> ，行 =% d 失败断言 = "% s"% s。 此错误可能与时间有关。 如果重新运行该语句后错误仍然存在，请使用 DBCC CHECKDB 来检查数据库的结构是否完整，或重新启动服务器以确保内存中的数据结构未破坏。|  
  
## <a name="explanation"></a>说明  
 与时间有关的暂时性错误或内存中或磁盘上的数据损坏均可导致此错误。  
  
## <a name="user-action"></a>用户操作  
 重新运行导致激发异常的语句。 如果错误是由与时间有关的事件导致的，则此错误可能不会重复发生。 如果问题仍然存在，请运行 DBCC CHECKDB 检查磁盘上的数据是否损坏。 重新启动服务器以确保内存中的数据结构未损坏。  
  
## <a name="see-also"></a>另请参阅  
 [DBCC CHECKDB (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
  
