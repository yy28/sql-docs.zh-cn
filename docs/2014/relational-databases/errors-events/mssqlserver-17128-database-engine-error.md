---
title: MSSQLSERVER_17128 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17128 (Database Engine error)
ms.assetid: 7b15a5e6-fd41-47ce-ba87-54f72acea4bb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7a73f2469c38d611b95e3446e80755687f40346e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62869705"
---
# <a name="mssqlserver17128"></a>MSSQLSERVER_17128
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|17128|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|INIT_NOBUFSPACE|  
|消息正文|initdata:没有可用于核心缓冲区的内存。|  
  
## <a name="explanation"></a>解释  
 缓冲池的初始内存分配或预留失败，并且 SQL Server 退出。  
  
## <a name="user-action"></a>用户操作  
 通常是由在非常小的计算机（远小于最低系统要求）上启动 SQL Server 引起的。  
  
  
