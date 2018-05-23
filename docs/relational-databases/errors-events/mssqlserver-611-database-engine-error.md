---
title: MSSQLSERVER_611 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 611 (Database Engine error)
ms.assetid: ac6a213f-5c38-44ad-bc85-a62863786614
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e118451f77e736da34edad35d7e1c64ec95bad37
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver611"></a>MSSQLSERVER_611
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
