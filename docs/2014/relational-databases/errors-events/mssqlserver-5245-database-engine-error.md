---
title: MSSQLSERVER_5245 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 5245 (Database Engine error)
ms.assetid: 6005c9ec-ccdd-4def-9eb4-37cdb599ddb3
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 64a63825586a603e2938cd57d98d38d555420dd6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014781"
---
# <a name="mssqlserver5245"></a>MSSQLSERVER_5245
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|5245|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC4_TABLE_LOCK_TIMEOUT_EXCEEDED|  
|消息正文|对象 ID O_ID (对象 'NAME'): 由于超过了锁请求超时期限，DBCC 无法获取该对象的锁。 已跳过此对象，不会处理它。|  
  
## <a name="explanation"></a>解释  
 在 DBCC 等待指定对象的表锁时，出现锁超时。  
  
## <a name="user-action"></a>用户操作  
 重新运行 DBCC 命令。  
  
  