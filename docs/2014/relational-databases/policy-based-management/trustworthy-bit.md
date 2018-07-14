---
title: 可信位 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3198188a-2b59-4865-9560-10f760934b8e
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 186a90bd7fa5884dea1887b6273338e16f76081e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37279066"
---
# <a name="trustworthy-bit"></a>可信位
  此规则确定数据库的 dbo 角色是否分配给了 sysadmin 固定服务器角色，以及数据库的可信位是否设置为 ON。  
  
 如果满足这些条件，特权数据库用户就可以提升 sysadmin 角色的特权。 在此角色中，用户可以创建和运行危害系统的不安全程序集。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 关闭可信位或者撤消 dbo 数据库角色的 sysadmin 权限。  
  
## <a name="for-more-information"></a>有关详细信息  
 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)  
  
## <a name="see-also"></a>请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
