---
title: MSSQLSERVER_15661 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 15661 (Database Engine error)
ms.assetid: 88b01bfb-74ce-4aa0-aec0-7885261c7ef3
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: bba24fb998afb3713de138c1c77f7a15bf04d100
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver15661"></a>MSSQLSERVER_15661
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|15661|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLErrorNum15661|  
|消息正文|sp_estimate_data_compression_savings 存储过程不能用于临时表。|  
  
## <a name="explanation"></a>解释  
临时表已用作 sp_estimate_data_compression_savings 存储过程的参数。 尽管支持压缩临时表，但 sp_estimate_data_compression_savings 不能用于估计压缩的存储内容。  
  
## <a name="user-action"></a>用户操作  
删除用作 sp_estimate_data_compression_savings 参数的临时表。  
  
