---
title: Shared Memory 属性 |Microsoft Docs
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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62999541"
---
# <a name="shared-memory-properties"></a>shared memory 属性
  使用“共享内存属性”对话框的“协议”页可以启用或禁用共享内存协议。 Shared Memory 是可供使用的最简单协议，没有可配置的设置。 由于使用 Shared Memory 协议的客户端仅可以连接到在同一台计算机运行的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，因此它对于大多数数据库活动而言是没有用的。 如果怀疑其他协议配置有误，请使用 Shared Memory 协议进行故障排除。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 才能启用或禁用该协议。  
  
## <a name="options"></a>选项  
 **已启用**  
 可能的值为“是”和“否”。 默认情况下，Shared Memory 协议是启用的。  
  
## <a name="see-also"></a>请参阅  
 [选择网络协议](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)   
 [使用 Shared Memory 协议创建有效的连接字符串](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
  
