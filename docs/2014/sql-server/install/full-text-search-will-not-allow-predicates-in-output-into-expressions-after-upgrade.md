---
title: 在升级后，全文搜索不会允许谓词中 OUTPUT INTO 表达式 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f6473409-121a-414d-8fe9-ea9aea6cb7eb
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 444f111de4d4672ad1127ccd775bf667743c70b7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015832"
---
# <a name="after-upgrade-full-text-search-will-not-allow-predicates-in-output-into-expression"></a>升级后，全文搜索将不再允许 OUTPUT INTO 表达式中使用谓词
  当数据库兼容级别设置为 100 或更高时，不允许在 OUTPUT 子句中使用全文谓词。  
  
## <a name="description"></a>Description  
 有关 OUTPUT 子句的详细信息，请参阅[OUTPUT 子句&#40;TRANSACT-SQL&#41;](/sql/t-sql/queries/output-clause-transact-sql)。  
  
## <a name="see-also"></a>请参阅  
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [全文搜索升级问题](../../../2014/sql-server/install/full-text-search-upgrade-issues.md)  
  
  
