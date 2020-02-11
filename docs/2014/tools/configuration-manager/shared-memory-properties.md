---
title: 共享内存属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- shared memory [SQL Server]
ms.assetid: dc1704da-eacd-4d26-b529-c996f958ca4b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bea56ada3ef490225fd08892128abb482b9342a8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62999541"
---
# <a name="shared-memory-properties"></a>shared memory 属性
  使用“共享内存属性”对话框的“协议”页可以启用或禁用共享内存协议。******** Shared Memory 是可供使用的最简单协议，没有可配置的设置。 由于使用 shared memory 协议的客户端只能连接到[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在同一台计算机上运行的实例，因此它对于大多数数据库活动而言不起作用。 如果怀疑其他协议配置有误，请使用 Shared Memory 协议进行故障排除。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]必须重新启动才能启用或禁用该协议。  
  
## <a name="options"></a>选项  
 **已启用**  
 可能的值为“是”  和“否”  。 默认情况下，Shared Memory 协议是启用的。  
  
## <a name="see-also"></a>另请参阅  
 [选择网络协议](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)   
 [使用 Shared Memory 协议创建有效的连接字符串](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
  
