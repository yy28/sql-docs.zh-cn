---
title: "系统数据库中的对称密钥 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: 28e25ae3-d3dc-45ec-b316-f219512a1a47
caps.latest.revision: "7"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ab1e853380ad3ec9cee539e664ac15e90ef4b494
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="symmetric-keys-on-system-databases"></a>系统数据库中的对称密钥
  此规则检查 master、msdb、model 和 tempdb 数据库中是否存在用户创建的对称密钥。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 请勿在系统数据库中创建对称密钥。  
  
## <a name="for-more-information"></a>有关详细信息  
 [选择加密算法](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
