---
title: MSSQLSERVER_3937 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3937 (Database Engine error)
ms.assetid: 312d5bbe-c8de-42db-af4b-4ccb448ce6ef
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 819db3b9668aaf8339108ffedaf31fd4db513e5f
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551523"
---
# <a name="mssqlserver_3937"></a>MSSQLSERVER_3937
    
## <a name="details"></a>详细信息  
  
|Attribute|值|  
|-|-|  
|产品名称|MSSQLSERVER|  
|事件 ID|3937|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|XACT_FILESTREAM_ROLLBACK_ERROR|  
|消息正文|在试图通知 FILESTREAM 筛选器驱动程序某事务已回滚时出错。 错误代码:0x%0x。|  
  
## <a name="explanation"></a>说明  
 发出有关某事务的回滚通知时，RsFx 驱动程序返回错误。 这可能是因资源不足而造成的。 这可能会导致 RsFx 筛选器驱动程序发生少量内存泄漏，但是，如果存在创建事务的 sqlservr.exe 进程，则可能不会发生这种情况。  
  
## <a name="user-action"></a>用户操作  
  
