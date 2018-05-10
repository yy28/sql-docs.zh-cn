---
title: MSSQLSERVER_2539 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 2539 (Database Engine error)
ms.assetid: e638efcc-56f4-40f9-9740-17ef67b47d79
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ddd72855e71c308ea7bd96161a62c51454360c37
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver2539"></a>MSSQLSERVER_2539
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
