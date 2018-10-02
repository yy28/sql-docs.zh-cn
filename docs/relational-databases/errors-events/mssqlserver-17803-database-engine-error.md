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
ms.openlocfilehash: 9f4c8e064a92581c69a6cf2bd13fcf239749032b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47825544"
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
  
