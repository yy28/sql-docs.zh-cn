---
title: MSSQLSERVER_2539 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 2539 (Database Engine error)
ms.assetid: e638efcc-56f4-40f9-9740-17ef67b47d79
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 89c01c5e8b2cb8948edd1e3a6092d0662c670b92
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver2539"></a>MSSQLSERVER_2539
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|2539|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC_ALLOCATION_SUMMARY_FOR_DATABASE|  
|消息正文|在此数据库中，总区数 = EXTENTS，已用页数 = USED_PAGES，保留页数 = RESERVED_PAGES。|  
  
## <a name="explanation"></a>解释  
此信息是 DBCC CHECKALLOC 命令输出的一部分。 此信息是指定数据库的已分配区数、已用页数和保留页数的摘要。  
  
## <a name="user-action"></a>用户操作  
InclusionThresholdSetting  
  

