---
title: Named Pipes 属性 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: configuration-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- pipes [SQL Server]
- listening [SQL Server], pipes
- pipes [SQL Server], listening on pipes
- Named Pipes [SQL Server], listening on pipes
ms.assetid: a5fd5b8e-f889-485b-89e3-d4010ec4c6ec
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a57aa95a44efa8c338d946a6eeebd186c2be858a
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MTE
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="named-pipes-properties"></a>Named Pipes 属性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  在使用 Named Pipes 协议时，可以使用“Named Pipes 属性”对话框的“协议”页查看或更改 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]侦听的命名管道。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 才能启用或禁用该协议，或更改命名管道。  
  
## <a name="options"></a>“常规”  
 **已启用**  
 可能的值为“是”和“否”。  
  
 **管道名称**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 侦听的命名管道。 默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 侦听： `\\.\pipe\sql\query` （对于默认实例）和 `\\.\pipe\MSSQL$<instancename>\sql\query` （对于命名实例）。 此字段最多允许 2047 个字符。  
  
## <a name="creating-an-alternate-named-pipe"></a>创建备用命名管道  
 若要更改命名管道，可以在 **“管道名称”** 框中键入新的管道名称，然后停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，再将其重新启动。 由于 **sql\query** 众所周知是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用的命名管道，更改管道可以有效地降低恶意程序攻击的风险。  
  
### <a name="example"></a>示例  
 键入 **\\\\.\pipe\unit\app** 以侦听 **unit\app** 管道。  
  
 键入 **\\\\.\pipe\acct** 以侦听 **acct** 管道。  
  
## <a name="see-also"></a>另请参阅  
 [启用或禁用服务器网络协议](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [选择网络协议](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [使用 Named Pipes 创建有效的连接字符串](http://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)  
  
  
