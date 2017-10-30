---
title: MSSQLSERVER_9692 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 9692 (Database Engine error)
ms.assetid: 02399d6e-ab5e-4f30-8a3e-2bb1e8c135b5
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 970733fb1f494b201e0bffa3f88aa27de4465cbf
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver9692"></a>MSSQLSERVER_9692
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|9692|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SB2_CANT_LISTEN_PORT_IN_USE|  
|消息正文|%S_MSG 协议传输无法侦听端口 %d，因为其他进程正在使用此端口。|  
  
## <a name="explanation"></a>解释  
计算机上的其他程序正在使用指示的 TCP 端口。  
  
## <a name="user-action"></a>用户操作  
运行 **netstat -aon** 以确定哪个程序正在使用该端口。 禁用该应用程序，或者为 Service Broker 指定其他端口。  
  

