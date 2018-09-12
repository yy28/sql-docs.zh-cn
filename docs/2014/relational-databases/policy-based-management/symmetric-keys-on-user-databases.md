---
title: 用户数据库中的对称密钥 | Microsoft Docs
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
ms.assetid: 3333ab5b-2518-4753-a0a8-57df5e5af74f
caps.latest.revision: 5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bc7ad34802993b402d2799767e93c0bccf30203e
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43814703"
---
# <a name="symmetric-keys-on-user-databases"></a>用户数据库中的对称密钥
  此规则检查长度小于 128 个字节的密钥是否没有使用 RC2 或 RC4 加密算法。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 使用 AES 128 位或更大位为数据加密创建对称密钥。 如果您的操作系统不支持 AES，请使用 3DES。  
  
## <a name="for-more-information"></a>有关详细信息  
 [选择加密算法](../security/encryption/choose-an-encryption-algorithm.md)  
  
## <a name="see-also"></a>请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
