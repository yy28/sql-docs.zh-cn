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
manager: craigg
ms.openlocfilehash: c48e0671052d612a52703aa7d367e03257cf1e14
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51667336"
---
# <a name="set-the-autoshrink-database-option-to-off"></a>将 AUTO_SHRINK 数据库选项设置为 OFF
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此规则检查 AUTO_SHRINK 数据库选项是否已设置为 OFF。 频繁收缩和展开数据库可能会导致物理碎片。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 将 AUTO_SHRINK 数据库选项设置为 OFF。 如果您知道以后将不再需要要回收的空间，则可以通过手动收缩数据库来回收该空间。  
  
## <a name="for-more-information"></a>有关详细信息  
 Microsoft 知识库文章 [315512](https://go.microsoft.com/fwlink/?linkid=117750)  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
