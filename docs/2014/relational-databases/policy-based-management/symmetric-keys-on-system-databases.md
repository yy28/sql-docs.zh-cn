---
title: 系统数据库中的对称密钥 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 28e25ae3-d3dc-45ec-b316-f219512a1a47
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5ac7d41bc693813f471caff7e746a44184146962
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52774799"
---
# <a name="symmetric-keys-on-system-databases"></a>系统数据库中的对称密钥
  此规则检查 master、msdb、model 和 tempdb 数据库中是否存在用户创建的对称密钥。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 请勿在系统数据库中创建对称密钥。  
  
## <a name="for-more-information"></a>有关详细信息  
 [选择加密算法](../security/encryption/choose-an-encryption-algorithm.md)  
  
## <a name="see-also"></a>请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
