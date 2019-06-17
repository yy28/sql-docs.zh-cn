---
title: MSSQLSERVER_233 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "233"
helpviewer_keywords:
- 233 (Database Engine error)
ms.assetid: 201665dc-7ac8-4c19-90d3-33354c5caa72
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4e18ce61356947754423cfb878cf47f90534b40f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62869217"
---
# <a name="mssqlserver233"></a>MSSQLSERVER_233
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|233|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称||  
|消息正文|已成功与服务器建立连接，但是在登录过程中发生错误。 (提供程序：共享内存提供程序，错误: 0 - 在管道的另一端没有进程。) (Microsoft SQL Server，错误: 233)|  
  
## <a name="explanation"></a>解释  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端无法连接到服务器。 发生此错误的原因可能是服务器未配置为接受远程连接。  
  
## <a name="user-action"></a>用户操作  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器工具使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接受远程连接。  
  
## <a name="see-also"></a>请参阅  
 [网络协议和网络库](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [客户端网络配置](../../database-engine/configure-windows/client-network-configuration.md)   
 [配置客户端协议](../../database-engine/configure-windows/configure-client-protocols.md)   
 [启用或禁用服务器网络协议](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
  
