---
title: MSSQLSERVER_3619 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3619 (Database Engine error)
ms.assetid: 7d94f8d9-65ca-4fde-9c17-7b83e94a3779
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6a82902d69a1d5214b29f43d19ded58c76293ec4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48047378"
---
# <a name="mssqlserver3619"></a>MSSQLSERVER_3619
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|3619|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SYS_NOLOG|  
|消息正文|由于日志空间用尽，无法在数据库 ID %d 中写入检查点记录。 请与数据库管理员联系，截断日志或为数据库日志文件分配更多空间。|  
  
## <a name="explanation"></a>解释  
 事务日志的磁盘空间不足。  
  
## <a name="user-action"></a>用户操作  
 截断日志以释放一些空间，或者为日志分配更多的空间。 有关详细信息，请参阅 Server SQL 联机丛书中的“解决事务日志已满的问题（错误 9002）”。  
  
  
