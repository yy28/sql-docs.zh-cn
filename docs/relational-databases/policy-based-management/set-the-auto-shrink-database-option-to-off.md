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
ms.openlocfilehash: fac9ff925c5e24d21efe0dcb5b7776636cf78572
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774191"
---
# <a name="set-the-auto_shrink-database-option-to-off"></a>将 AUTO_SHRINK 数据库选项设置为 OFF
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  此规则检查 AUTO_SHRINK 数据库选项是否已设置为 OFF。 频繁收缩和展开数据库可能会导致物理碎片。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 将 AUTO_SHRINK 数据库选项设置为 OFF。 如果您知道以后将不再需要要回收的空间，则可以通过手动收缩数据库来回收该空间。  
  
## <a name="for-more-information"></a>有关详细信息  
 Microsoft 知识库文章 [315512](https://go.microsoft.com/fwlink/?linkid=117750)  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来监视和强制执行最佳做法](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
