---
title: MSSQLSERVER_8443 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 8443 (Database Engine error)
ms.assetid: a3541b9c-b1a8-4280-add1-275f08696b62
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ff486acfff1f68078e702ec792ecfc09aba006d5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver8443"></a>MSSQLSERVER_8443
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|8443|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SB_DIALOG_WO_CONV_GROUP|  
|消息正文|ID 为 '%.*ls' 且发起方为 %d 的会话引用的会话组 '%.\*ls' 已丢失。 请运行 DBCC CHECKDB 以分析和修复数据库。|  
  
## <a name="explanation"></a>解释  
元数据层为会话组返回了 NULL。 数据库由于某个原因已损坏。 造成它损坏的一个可能原因是磁盘错误。  
  
## <a name="user-action"></a>用户操作  
在修复模式下运行 DBCC CHECKDB 使数据库回复到一致状态。 如果需要还原一致性，则它可能会删除消息。 调查系统错误日志以查看此错误是否由系统中的其他故障导致。  
  
