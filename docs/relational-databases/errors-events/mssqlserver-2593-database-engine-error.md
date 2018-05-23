---
title: MSSQLSERVER_2593 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 2593 (Database Engine error)
ms.assetid: 2e25bc43-606a-40de-8b87-3b55b96f4a91
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bb1c4cef6aa746a7d8db78d7d5c46db699207c8a
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver2593"></a>MSSQLSERVER_2593
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|2593|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC_OBJECT_ROW_PAGE_SUMMARY|  
|消息正文|对象 'object' 的 PAGECOUNT 页中有 ROWCOUNT 行。|  
  
## <a name="explanation"></a>解释  
此消息是所有 DBCC 检查（DBCC CHECKALLOC 除外）返回的信息性输出的一部分，指示指定对象的行和页计数。  
  
## <a name="user-action"></a>用户操作  
InclusionThresholdSetting  
  
