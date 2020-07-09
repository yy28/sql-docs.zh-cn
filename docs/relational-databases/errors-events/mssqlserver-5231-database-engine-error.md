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
ms.openlocfilehash: 6be551a13382279401648b1579b542a71142dd23
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717052"
---
# <a name="mssqlserver_5231"></a>MSSQLSERVER_5231
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|5231|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC4_DEADLOCK_SKIPPED_OBJECT|  
|消息正文|对象 ID O_ID （对象“NAME”）：尝试锁定此对象以进行检查时出现死锁。 已跳过此对象，不会处理它。|  
  
## <a name="explanation"></a>说明  
在 DBCC 尝试锁定该对象时出现死锁，而且 DBCC 被选作死锁牺牲品。 不会处理该对象。  
  
## <a name="user-action"></a>用户操作  
无  
  
