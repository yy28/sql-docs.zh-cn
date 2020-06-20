---
title: MSSQLSERVER_2511 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2511 (Database Engine error)
ms.assetid: 9a00c0ed-eb4b-4fae-8016-192396006c37
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 23e91b0d64140329639cf57f3a336cd2eab8e4e8
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85034508"
---
# <a name="mssqlserver_2511"></a>MSSQLSERVER_2511
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|2511|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC_KEYS_OUT_OF_ORDER|  
|消息正文|表错误: 对象 ID %d，索引 ID %d，分区 ID %I64d，分配单元 ID %I64d (类型为 %.*ls)。 页 %S_PGID，槽 %d 和 %d 中的键顺序不对。|  
  
## <a name="explanation"></a>说明  
 在指定的索引中检测到顺序不对的键。 包含这些键的页可能已损坏。  
  
## <a name="user-action"></a>用户操作  
 使用 ALTER INDEX REBUILD 语句重新生成指定的索引。  
  
  
