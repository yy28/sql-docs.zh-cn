---
title: "网络数据包大小不应超过 8060 字节 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 86db5da1-afe4-4fbb-8bf8-33cedc7e4361
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cb2e255e501d739ddfe8f822c7c62b212aa14db8
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="network-packet-size-should-not-exceed-8060-bytes"></a>网络数据包大小不应超过 8060 字节
  如果为 sp_configure 'network packet size' 指定的值或者任何登录用户的网络数据包大小大于 8060 字节， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将执行不同的内存分配操作。 这可能会增加不是为缓冲池保留的进程虚拟地址空间。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 网络数据包大小不应超过 8060 字节。  
  
## <a name="for-more-information"></a>有关详细信息  
 [Microsoft 知识库文章 903002](http://go.microsoft.com/fwlink/?linkid=117749)  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
