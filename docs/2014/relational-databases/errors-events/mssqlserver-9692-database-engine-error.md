---
title: MSSQLSERVER_9692 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9692 (Database Engine error)
ms.assetid: 02399d6e-ab5e-4f30-8a3e-2bb1e8c135b5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6b6ba95771aafffa5a322ffa1b7443419936addd
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053437"
---
# <a name="mssqlserver_9692"></a>MSSQLSERVER_9692
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|9692|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SB2_CANT_LISTEN_PORT_IN_USE|  
|消息正文|%S_MSG 协议传输无法侦听端口 %d，因为其他进程正在使用此端口。|  
  
## <a name="explanation"></a>说明  
 计算机上的其他程序正在使用指示的 TCP 端口。  
  
## <a name="user-action"></a>用户操作  
 运行 `netstat -aon` 以确定哪个程序正在使用该端口。 禁用该应用程序，或者为 Service Broker 指定其他端口。  
  
  
