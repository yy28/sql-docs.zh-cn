---
title: 用户数据库中的对称密钥 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3333ab5b-2518-4753-a0a8-57df5e5af74f
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: e8d11021d3e88aa62696d5cf1743359884fa672a
ms.sourcegitcommit: ef6e3ec273b0521e7c79d5c2a4cb4dcba1744e67
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2018
ms.locfileid: "51512492"
---
# <a name="symmetric-keys-on-user-databases"></a>用户数据库中的对称密钥
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此规则检查长度小于 128 个字节的密钥是否没有使用 RC2 或 RC4 加密算法。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 使用 AES 128 位或更大位为数据加密创建对称密钥。 如果您的操作系统不支持 AES，请使用 3DES。  
  
## <a name="for-more-information"></a>有关详细信息  
 [选择加密算法](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
