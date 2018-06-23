---
title: MSSQLSERVER_8966 | Microsoft Docs
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
- 8966 (Database Engine error)
ms.assetid: 6b1150fd-9dfd-4df9-8f08-8eca237667db
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 0db9faf0217e8f0d352f92547b5ba6c31631e64e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130134"
---
# <a name="mssqlserver8966"></a>MSSQLSERVER_8966
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|8966|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC3_FAILED_TO_READ_AND_LATCH_PAGE|  
|消息正文|无法使用闩锁类型 TYPE 读取并闩锁页 P_ID。 操作失败。|  
  
## <a name="explanation"></a>解释  
 页读取失败或无法针对 PFS 或 GAM 页进行闩锁。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志中可能会有闩锁超时或其他附带的消息。  
  
## <a name="user-action"></a>用户操作  
 查阅 SQL 错误日志，检查附带的消息并解决其中的错误。  
  
  