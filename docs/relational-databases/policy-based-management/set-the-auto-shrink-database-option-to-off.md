---
title: 将 AUTO_SHRINK 数据库选项设置为 OFF | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 16403850-d745-4754-b84f-5f01aaecd24e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2b202f2856e066047c5458ef8ed1f40b2422b391
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "68021689"
---
# <a name="set-the-auto_shrink-database-option-to-off"></a>将 AUTO_SHRINK 数据库选项设置为 OFF
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此规则检查 AUTO_SHRINK 数据库选项是否已设置为 OFF。 频繁收缩和展开数据库可能会导致物理碎片。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 将 AUTO_SHRINK 数据库选项设置为 OFF。 如果您知道以后将不再需要要回收的空间，则可以通过手动收缩数据库来回收该空间。  
  
## <a name="for-more-information"></a>有关详细信息  
 Microsoft 知识库文章 [315512](https://go.microsoft.com/fwlink/?linkid=117750)  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来监视和强制执行最佳做法](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
