---
title: MSSQLSERVER_7910 | Microsoft Docs
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
- 7910 (Database Engine error)
ms.assetid: 017a0113-2b17-40b3-a419-30bbc43d46b8
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 056802e0965e60963af5ec36bfc416c59cd0ff4f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126317"
---
# <a name="mssqlserver7910"></a>MSSQLSERVER_7910
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|7910|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC2_REPAIR_PAGE_ALLOCATED|  
|消息正文|修复: 页 P_ID 已分配给对象 ID O_ID，索引 ID I_ID，分区 ID PN_ID，分配单元 ID A_ID（类型为 TYPE）。|  
  
## <a name="explanation"></a>解释  
 这是来自 REPAIR 的信息性消息，指示页已分配给索引分配映射 (IAM) 页的单页槽数组。  
  
## <a name="user-action"></a>用户操作  
 InclusionThresholdSetting  
  
  