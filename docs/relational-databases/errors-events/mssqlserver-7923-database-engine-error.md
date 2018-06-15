---
title: MSSQLSERVER_7923 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 7923 (Database Engine error)
ms.assetid: b09a95e2-0ffe-4847-aa77-51e6639259f6
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 62880ac8bef9781af9a6a980c2895ffff65ecf65
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
ms.locfileid: "34325209"
---
# <a name="mssqlserver7923"></a>MSSQLSERVER_7923
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|7923|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC2_SUMMARY_TABLE_NAME|  
|消息正文|表 TABLE                对象 ID O_ID。|  
  
## <a name="explanation"></a>解释  
这是来自 DBCC CHECKALLOC 命令的信息性消息。 在该消息中，表中所有分配单元的分配信息列表顶部都包含表名和表 ID。  
  
## <a name="user-action"></a>用户操作  
InclusionThresholdSetting  
  
