---
title: 全文搜索断字符和筛选器显著改进了在 SQL Server 2005 和 SQL Server 2008 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- filters [Full-Text Search]
- word breakers [Full-Text Search]
ms.assetid: 8d06bda9-0bbf-4baa-b270-07b1c1f640eb
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d993c20ccd1af008f032b019c40bf673802d2f79
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026059"
---
# <a name="full-text-search-word-breakers-and-filters-significantly-improved-in-sql-server-2005-and-sql-server-2008"></a>全文搜索断字符和筛选器在 SQL Server 2005 和 SQL Server 2008 中有重大改进
  断字符和筛选器都进行了重大更改。 对断字符进行了更多改进，其中包括增强的语言覆盖范围和可靠性。  
  
## <a name="description"></a>Description  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 全文搜索使用的断字符和筛选器经过了重大修改，从而使功能和可靠性都得到提高。 在某些特定情况下，对断字符所做的更改可能会影响某些数据的词汇切分方式。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中创建的标记可能与 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 或 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中创建的早期标记不同。  
  
 有关断字符的信息，请参阅[配置和管理断字符和词干分析器以便搜索](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)。  
  
## <a name="see-also"></a>请参阅  
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  