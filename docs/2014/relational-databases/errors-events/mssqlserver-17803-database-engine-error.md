---
title: MSSQLSERVER_17803 | Microsoft Docs
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
- 17803 (Database Engine error)
ms.assetid: 28591a19-258d-4891-b78a-4686789bb2d7
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b7a2ab967786eaa05c8ac393bbeaf0e42164f0f6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123862"
---
# <a name="mssqlserver17803"></a>MSSQLSERVER_17803
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|17803|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SRV_NOMEMORY|  
|消息正文|在建立连接过程中出现内存分配错误。 减少不必要的内存负载，或增加系统内存。 该连接已关闭。%.*ls|  
  
## <a name="explanation"></a>解释  
 服务器内存不足。  
  
## <a name="user-action"></a>用户操作  
 确定服务器内存不足的原因。 一般内存故障排除步骤可能会很有用  
  
  