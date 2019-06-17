---
title: MSSQLSERVER_10061 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "10061"
helpviewer_keywords:
- 10061 (Database Engine error)
ms.assetid: 729602f3-08df-474c-8740-8dea13c1eee3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b77e1d920f97891d173bfdcdcb23ceb6c0acf0c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62870705"
---
# <a name="mssqlserver10061"></a>MSSQLSERVER_10061
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10061|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称||  
|消息正文|在建立与服务器的连接时出错。  在连接到 SQL Server 时，在默认的设置下 SQL Server 不允许远程连接可能会导致此失败。 (提供程序：TCP 提供程序，错误:0 - 因目标计算机主动拒绝该连接而导致无法建立连接。) (Microsoft SQL Server，错误:10061)|  
  
## <a name="explanation"></a>解释  
 服务器未响应客户端请求。 发生此错误的原因可能是尚未启动服务器。  
  
## <a name="user-action"></a>用户操作  
 确保已启动服务器。  
  
## <a name="see-also"></a>请参阅  
 [管理数据库引擎服务](../../database-engine/configure-windows/manage-the-database-engine-services.md)   
 [配置客户端协议](../../database-engine/configure-windows/configure-client-protocols.md)   
 [网络协议和网络库](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [客户端网络配置](../../database-engine/configure-windows/client-network-configuration.md)   
 [配置客户端协议](../../database-engine/configure-windows/configure-client-protocols.md)   
 [启用或禁用服务器网络协议](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
  
