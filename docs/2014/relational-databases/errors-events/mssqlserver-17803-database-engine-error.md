---
title: MSSQLSERVER_17803 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17803 (Database Engine error)
ms.assetid: 28591a19-258d-4891-b78a-4686789bb2d7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 683806941947a6da888264e4d0e4e3807200ef13
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62869542"
---
# <a name="mssqlserver17803"></a>MSSQLSERVER_17803
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
