---
title: MSSQLSERVER_5231 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5231 (Database Engine error)
ms.assetid: 6954ae84-ed0b-4f4c-9d0a-e73f3d71476c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 998bf914523dec7012c6d9e84d89de858173ba38
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47709215"
---
# <a name="mssqlserver5231"></a>MSSQLSERVER_5231
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|5231|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC4_DEADLOCK_SKIPPED_OBJECT|  
|消息正文|对象 ID O_ID（对象 'NAME'）: 尝试锁定此对象以进行检查时出现死锁。 已跳过此对象，不会处理它。|  
  
## <a name="explanation"></a>解释  
在 DBCC 尝试锁定该对象时出现死锁，而且 DBCC 被选作死锁牺牲品。 不会处理该对象。  
  
## <a name="user-action"></a>用户操作  
None  
  
