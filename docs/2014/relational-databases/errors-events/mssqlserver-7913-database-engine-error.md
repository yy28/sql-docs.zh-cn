---
title: MSSQLSERVER_7913 | Microsoft Docs
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
- 7913 (Database Engine error)
ms.assetid: 9d8ad456-b1a2-4f79-a252-657fbec9ad9b
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 88c8b531b994cfce0114420a94b748c8a8f509c1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024569"
---
# <a name="mssqlserver7913"></a>MSSQLSERVER_7913
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|7913|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC2_REPAIR_EXTENT_DEALLOCATED|  
|消息正文|修复：区 P_ID 已从对象 ID O_ID，索引 ID I_ID，分区 ID PN_ID，分配单元 ID A_ID (类型为 TYPE)释放。|  
  
## <a name="explanation"></a>解释  
 这是来自 REPAIR 的信息性消息，该消息声明已将一个区从指定的对象释放。  
  
## <a name="user-action"></a>用户操作  
 InclusionThresholdSetting  
  
  