---
title: MSSQLSERVER_2538 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2538 (Database Engine error)
ms.assetid: 0a0f7d79-f1ba-4749-8804-fb660cca3492
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 44de009a70cfca53e6961fd1c06d7b39a1b8affd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63045847"
---
# <a name="mssqlserver2538"></a>MSSQLSERVER_2538
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|2538|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC_ALLOCATION_SUMMARY_PER_FILE|  
|消息正文|文件 FILE。 区数 = EXTENTS，已用页数 = USED_PAGES，保留页数 = RESERVED_PAGES。|  
  
## <a name="explanation"></a>解释  
此信息是 DBCC CHECKALLOC 命令输出的一部分。 此信息是指定数据库的已分配区数、已用页数和保留页数的按文件摘要。  
  
## <a name="user-action"></a>用户操作  
None  
  
