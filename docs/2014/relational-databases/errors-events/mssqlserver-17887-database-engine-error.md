---
title: MSSQLSERVER_17887 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17887 (Database Engine error)
ms.assetid: ad0806e6-3296-4c32-b103-fccf0f8a8d3d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b889779da7f48ffd52d55c63e2ddb0742c065e59
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553502"
---
# <a name="mssqlserver_17887"></a>MSSQLSERVER_17887
    
## <a name="details"></a>详细信息  
  
|Attribute|值|  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|17887|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SRV_IO_COMP_LISTENER_NONYIELDING|  
|消息正文|节点 %ld 上的 IO 完成侦听器(0x%lx)工作线程 0x%p 似乎无法完成。 CPU 近似使用时间: 内核 %I64d 毫秒，用户 %I64d 毫秒，间隔: %I64d。|  
  
## <a name="explanation"></a>说明  
 指示当为某一网络读/写事件执行 I/O 完成例程时，指定节点上的 I/O 完成端口侦听器可能出现了问题。 当 I/O 完成端口侦听器从执行 I/O 完成例程返回时，此错误将消失。  
  
## <a name="user-action"></a>用户操作  
 请与 Microsoft 客户支持服务部门 (CSS) 联系。  
  
  
