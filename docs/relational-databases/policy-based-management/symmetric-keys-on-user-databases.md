---
title: 用户数据库中的对称密钥 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3333ab5b-2518-4753-a0a8-57df5e5af74f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 213ae962f1dbc45d9e6fc2bed67c94f2eafb1183
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601735"
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
  
  
