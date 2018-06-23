---
title: 将 AUTO_SHRINK 数据库选项设置为 OFF | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 16403850-d745-4754-b84f-5f01aaecd24e
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d672ff1be6102477bff51dd71b9d26a98e386c8c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129658"
---
# <a name="set-the-autoshrink-database-option-to-off"></a>将 AUTO_SHRINK 数据库选项设置为 OFF
  此规则检查 AUTO_SHRINK 数据库选项是否已设置为 OFF。 频繁收缩和展开数据库可能会导致物理碎片。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 将 AUTO_SHRINK 数据库选项设置为 OFF。 如果您知道以后将不再需要要回收的空间，则可以通过手动收缩数据库来回收该空间。  
  
## <a name="for-more-information"></a>有关详细信息  
 Microsoft 知识库文章 [315512](http://go.microsoft.com/fwlink/?linkid=117750)  
  
## <a name="see-also"></a>请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  