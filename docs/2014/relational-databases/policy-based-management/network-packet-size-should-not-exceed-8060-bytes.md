---
title: 网络数据包大小不应超过 8060 字节 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 86db5da1-afe4-4fbb-8bf8-33cedc7e4361
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1a4e25b746305cc3f8575f167cc9a216491ac55f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126197"
---
# <a name="network-packet-size-should-not-exceed-8060-bytes"></a>网络数据包大小不应超过 8060 字节
  如果为 sp_configure 'network packet size' 指定的值或者任何登录用户的网络数据包大小大于 8060 字节， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将执行不同的内存分配操作。 这可能会增加不是为缓冲池保留的进程虚拟地址空间。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 网络数据包大小不应超过 8060 字节。  
  
## <a name="for-more-information"></a>有关详细信息  
 [Microsoft 知识库文章 903002](http://go.microsoft.com/fwlink/?linkid=117749)  
  
## <a name="see-also"></a>请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
