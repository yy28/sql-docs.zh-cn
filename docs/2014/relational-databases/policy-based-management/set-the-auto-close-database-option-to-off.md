---
title: 将 AUTO_CLOSE 数据库选项设置为 OFF | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: e6b03364-263a-4ec4-9794-de9869d396ce
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 43cabd1eed4aaf84cb510428310c4c778a7d947c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48076547"
---
# <a name="set-the-autoclose-database-option-to-off"></a>将 AUTO_CLOSE 数据库选项设置为 OFF
  此规则检查 AUTO_ CLOSE 选项是否设置为 OFF。 AUTO_CLOSE 设置为 ON 时，该选项可能导致频繁访问数据库而使性能下降，这是因为在每次连接后打开和关闭数据库增加了开销。 AUTO_CLOSE 还会在每次连接后刷新过程缓存。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 如果频繁访问数据库，则将数据库的 AUTO_CLOSE 选项设置为 OFF。  
  
## <a name="for-more-information"></a>有关详细信息  
 [ALTER DATABASE SET 选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
  
## <a name="see-also"></a>请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
