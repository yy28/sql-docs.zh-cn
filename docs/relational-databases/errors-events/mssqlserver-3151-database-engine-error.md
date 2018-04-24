---
title: MSSQLSERVER_3151 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 3151 (Database Engine error)
ms.assetid: a8657a91-ec75-4649-a09a-21920e0030ff
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2a91804459fb6ad8b56e445bdaf3810985c88a22
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver3151"></a>MSSQLSERVER_3151
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|3151|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|LDDB_MASTER_LOAD_FAILED|  
|消息正文|无法还原 master 数据库。 正在关闭 SQL Server。 请检查错误日志，然后重新生成 master 数据库。 有关如何重新生成 master 数据库的详细信息，请参阅 SQL Server 联机丛书。|  
  
## <a name="explanation"></a>解释  
这是一般的错误消息，指示 **master** 数据库存在各种问题。  
  
## <a name="user-action"></a>用户操作  
检查错误日志以了解详细信息。 若要创建可用的 **master** 数据库，请使用 REBUILDDATABASE 选项运行 Setup.exe。 有关详细信息，请参阅 SQL Server 联机丛书中的“如何从命令提示符安装 SQL Server”。  
  
