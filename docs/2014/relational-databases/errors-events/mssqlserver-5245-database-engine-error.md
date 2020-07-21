---
title: MSSQLSERVER_5245 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 5245 (Database Engine error)
ms.assetid: 6005c9ec-ccdd-4def-9eb4-37cdb599ddb3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2cea5c900150a26ecde783e50b953cc4a035a8ff
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551214"
---
# <a name="mssqlserver_5245"></a>MSSQLSERVER_5245
    
## <a name="details"></a>详细信息  
  
|Attribute|值|  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|5245|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC4_TABLE_LOCK_TIMEOUT_EXCEEDED|  
|消息正文|对象 ID O_ID （对象“NAME”）：由于超过了锁请求超时期限，DBCC 无法获取该对象的锁。 已跳过此对象，不会处理它。|  
  
## <a name="explanation"></a>说明  
 在 DBCC 等待指定对象的表锁时，出现锁超时。  
  
## <a name="user-action"></a>用户操作  
 重新运行 DBCC 命令。  
  
  
