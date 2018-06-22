---
title: MSSQLSERVER_611 | Microsoft Docs
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
- 611 (Database Engine error)
ms.assetid: ac6a213f-5c38-44ad-bc85-a62863786614
caps.latest.revision: 19
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: fc1a8b3bc8f492e73b543ce7551dfba52a1dbd55
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015233"
---
# <a name="mssqlserver611"></a>MSSQLSERVER_611
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|611|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|VAR_SIZE_TOO_BIG|  
|消息正文|无法插入或更新行，因为总可变列大小(包括系统开销)比限值多出 %d 个字节。|  
  
## <a name="explanation"></a>解释  
 最大可变列大小超过架构所允许的大小。 当可变列超过启用 vardecimal 存储格式时的固定列大小限制，或可变列大小超过 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 对压缩数据记录所允许的限制时，将返回错误 611。  
  
## <a name="user-action"></a>用户操作  
 减小记录的大小。  
  
  