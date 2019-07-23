---
title: 共享内存属性 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- shared memory [SQL Server]
ms.assetid: dc1704da-eacd-4d26-b529-c996f958ca4b
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 17a251e25eaf02ee0733f6d00a077bd4706db29a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058336"
---
# <a name="shared-memory-properties"></a>shared memory 属性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  使用“共享内存属性”对话框的“协议”页可以启用或禁用共享内存协议。   Shared Memory 是可供使用的最简单协议，没有可配置的设置。 由于使用 Shared Memory 协议的客户端仅可以连接到在同一台计算机运行的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，因此它对于大多数数据库活动而言是没有用的。 如果怀疑其他协议配置有误，请使用 Shared Memory 协议进行故障排除。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 才能启用或禁用该协议。  
  
## <a name="options"></a>选项  
 **已启用**  
 可能的值为“是”  和“否”  。 默认情况下，Shared Memory 协议是启用的。  
  
## <a name="see-also"></a>另请参阅  
 [选择网络协议](https://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [使用 Shared Memory 协议创建有效的连接字符串](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
  
