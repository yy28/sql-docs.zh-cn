---
description: MSSQLSERVER_5245
title: MSSQLSERVER_5245 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5245 (Database Engine error)
ms.assetid: 6005c9ec-ccdd-4def-9eb4-37cdb599ddb3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 67ae97cdfc3e6db07870844e418eacc07c4c857f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470975"
---
# <a name="mssqlserver_5245"></a>MSSQLSERVER_5245
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
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
  
