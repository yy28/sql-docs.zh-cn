---
title: 客户端协议属性（"顺序" 选项卡） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- client protocols [SQL Server]
ms.assetid: 64fd7135-1756-4885-bed9-9ab8997ecc6c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cb3055780186c34f6ead494f702874fbc6329f5b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63044173"
---
# <a name="client-protocols-properties-order-tab"></a>客户端协议属性（“顺序”选项卡）
  使用“客户端协议属性”**** 对话框中的“顺序”**** 页，可以查看和启用客户端协议。  
  
 单击某个协议，再单击 **“启用”** 或 **“禁用”** ，可以将所选协议移到 **“启用的协议”** 列表或 **“禁用的协议”** 列表中。  
  
 按照列出的顺序尝试协议，首先尝试使用顶级协议进行连接，然后尝试使用第二个列出的协议进行连接，等等。通过单击向上键和向下箭头按钮，在 "**已启用的协议**" 列表中向上或向下移动协议。 从该计算机上的客户端连接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，将始终首先尝试使用 **“Shared Memory”** 协议（如果已启用）。  
  
> [!NOTE]  
>  
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET SqlClient 不会使用这些设置。 .NET SqlClient 的协议顺序依次为：TCP、命名管道。此顺序不能改变。  
  
## <a name="options"></a>选项  
 **“启用的协议”**  
 列出已安装但当前未使用的协议。  
  
 **“禁用的协议”**  
 列出此计算机上的[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端可以使用的协议。  
  
 **>**  
 启用“禁用的协议”**** 框中当前突出显示的协议，会将其移到“启用的协议”**** 框中。  
  
 **\<**  
 禁用“启用的协议”**** 框中当前突出显示的协议，会将其移到“禁用的协议”**** 框中。  
  
 向上键  
 在列表中向上移动突出显示的协议。 这样就可以使网络库尝试使用所选协议进行连接的优先级提高。  
  
 向下键  
 在列表中向下移动突出显示的协议。 这样就可以使网络库尝试使用所选协议进行连接的优先级降低。  
  
 **启用 Shared Memory 协议**  
 从该计算机上的客户端连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，启用 Shared Memory 协议。在启用了该协议的情况下，始终首先尝试使用该协议。  
  
> [!NOTE]  
>  如果通过前缀或连接字符串的一部分指定了协议，则仅尝试使用指定的协议。  
  
## <a name="see-also"></a>另请参阅  
 [选择网络协议](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
