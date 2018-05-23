---
title: MSSQLSERVER_7916 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 7916 (Database Engine error)
ms.assetid: 9bac3536-de14-4e98-84c2-bde9a59ba0d1
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 48636c3800e93fba33c5371d7e78eafed8bc926d
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver7916"></a>MSSQLSERVER_7916
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|7916|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC2_REPAIR_RECORD|  
|消息正文|修复: 对象 ID O_ID，索引 ID I_ID，分区 ID PN_ID，分配单元 ID A_ID (类型为 TYPE)，页 P_ID，槽 S_ID 的记录已删除。 将重新生成索引。|  
  
## <a name="explanation"></a>解释  
这是来自 REPAIR 的信息性消息，指示已将指定记录从页中删除。  
  
## <a name="user-action"></a>用户操作  
InclusionThresholdSetting  
  
