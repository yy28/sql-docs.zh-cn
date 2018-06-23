---
title: MSSQLSERVER_2539 | Microsoft Docs
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
- 2539 (Database Engine error)
ms.assetid: e638efcc-56f4-40f9-9740-17ef67b47d79
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 9d346c85523bdcfd6e5ebd9f4aec5ba044b7d3b4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018881"
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
  
  