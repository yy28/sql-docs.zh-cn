---
title: 网络数据包大小不应超过 8060 字节 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 86db5da1-afe4-4fbb-8bf8-33cedc7e4361
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3652e83a63a088d2af0e26c401d30484df5c76b0
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43811403"
---
# <a name="network-packet-size-should-not-exceed-8060-bytes"></a>网络数据包大小不应超过 8060 字节
  如果为 sp_configure 'network packet size' 指定的值或者任何登录用户的网络数据包大小大于 8060 字节， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将执行不同的内存分配操作。 这可能会增加不是为缓冲池保留的进程虚拟地址空间。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 网络数据包大小不应超过 8060 字节。  
  
## <a name="for-more-information"></a>有关详细信息  
 [Microsoft 知识库文章 903002](http://go.microsoft.com/fwlink/?linkid=117749)  
  
## <a name="see-also"></a>请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
