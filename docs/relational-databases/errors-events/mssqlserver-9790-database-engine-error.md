---
title: MSSQLSERVER_9790 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 9790 (Database Engine error)
ms.assetid: 83fd379f-5deb-4f97-8cb4-282e3d3fed94
caps.latest.revision: 13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5b737472be9bea3ac2a8e9e9a2fb393851dca457
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver9790"></a>MSSQLSERVER_9790
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|9790|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SB3_XMIT_ERROR_ENTRANCE_BROKER_SINGLE_USER|  
|消息正文|无法确定传入消息的路由。 包含路由信息的系统数据库 MSDB 处于 SINGLE USER 模式。|  
  
## <a name="explanation"></a>解释  
尝试对从网络接收的消息进行分类时出错，因为 MSDB 数据库处于 SINGLE USER 模式。  
  
## <a name="user-action"></a>用户操作  
使用 ALTER DATABASE 命令将 MSDB 更改为 MULTI USER 模式。  
  
