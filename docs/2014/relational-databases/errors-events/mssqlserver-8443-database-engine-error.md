---
title: MSSQLSERVER_8443 | Microsoft Docs
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
- 8443 (Database Engine error)
ms.assetid: a3541b9c-b1a8-4280-add1-275f08696b62
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: d6e7ccc935f09bf69e848ead0a906365eeb5fe2d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128054"
---
# <a name="mssqlserver8443"></a>MSSQLSERVER_8443
    
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
  
  