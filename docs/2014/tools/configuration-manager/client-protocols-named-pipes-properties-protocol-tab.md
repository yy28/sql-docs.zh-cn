---
title: 客户端协议 - 命名管道属性（“协议”选项卡）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- pipes [SQL Server], connecting to
- Named Pipes [SQL Server], default pipe
- client protocols [SQL Server]
ms.assetid: 30fbae62-2f2e-4d36-9c6e-3444fff68781
author: stevestein
ms.author: sstein
ms.openlocfilehash: 169b6d98212c724b8d6c43615ae2fa7eba9cfc7d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85008144"
---
# <a name="client-protocols---named-pipes-properties-protocol-tab"></a>客户端协议 - Named Pipes 属性（“协议”选项卡）
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器中，使用“Named Pipes 属性”  对话框中的“协议”  选项卡可以查看或修改默认管道的说明。 若要连接到其他管道，请在 **“默认管道”** 框中键入该管道。 有关连接字符串的详细信息，请参阅 [Creating a Valid Connection String Using Named Pipes](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-named-pipes.md)。  
  
## <a name="options"></a>选项  
 **“默认管道”**  
 指定 Named Pipes 网络库用来尝试连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目标实例的默认管道。 默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 侦听： `\\.\pipe\sql\query`  
  
 若要连接到默认管道，请输入 `sql\query`  
  
 **已启用**  
 可能的值为“是”  和“否”  。  
  
## <a name="see-also"></a>另请参阅  
 [选择网络协议](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
