---
title: MSSQLSERVER_17132 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 17132 (Database Engine error)
ms.assetid: d1d198bd-6730-4394-bd5f-28f320c01a38
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 2701e2c6207c146d9aeb75568659f5f8e6f3d4d4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver17132"></a>MSSQLSERVER_17132
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|17132|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|INIT_NODESSPACE|  
|消息正文|由于没有足够的内存可用于描述符，导致服务器启动失败。 请减少不重要的内存负载或增加系统内存。|  
  
## <a name="explanation"></a>解释  
无法分配足够的内存来存储服务器内部描述符。  
  
## <a name="user-action"></a>用户操作  
在计算机中添加更多内存。 一般内存故障排除步骤可能会非常有用。  
  
