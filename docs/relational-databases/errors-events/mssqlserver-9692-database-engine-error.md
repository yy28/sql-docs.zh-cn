---
title: MSSQLSERVER_9692 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9692 (Database Engine error)
ms.assetid: 02399d6e-ab5e-4f30-8a3e-2bb1e8c135b5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7041aa3e2262932541c4d81fe93dd1d9a740c97a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903817"
---
# <a name="mssqlserver9692"></a>MSSQLSERVER_9692
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
