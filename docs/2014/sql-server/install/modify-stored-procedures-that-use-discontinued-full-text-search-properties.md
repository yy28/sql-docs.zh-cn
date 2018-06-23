---
title: 修改使用废弃的全文搜索属性的存储的过程 |Microsoft 文档
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
- discontinued properties [Full-Text Search]
- stored procedures [Full-Text Search]
ms.assetid: 8d9392d9-a9ba-4378-84e4-59f516b67ddb
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 027fb2a7148dc0948c519836f30c8931d61f610b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025651"
---
# <a name="modify-stored-procedures-that-use-discontinued-full-text-search-properties"></a>修改使用已停用全文搜索属性的存储过程
  为确保存储过程正确执行，应编辑现有过程并删除已删除或已废弃的与全文相关的属性和设置。  
  
## <a name="component"></a>组件  
 全文搜索  
  
## <a name="description"></a>Description  
 以下与全文搜索相关的属性和设置已删除。  
  
-   **DataTimeout**  
  
-   **ConnectTimeout**  
  
-   **Clean_up**  
  
-   **LogSize**  
  
 以下与全文搜索相关的属性和设置已删除或已废弃：  
  
-   全文目录的“路径”。 全文目录将是在系统中没有特定文件路径的一个逻辑对象。  
  
-   在 SP_FULLTEXT_DATABASE 中启用/禁用全文检索不会再产生任何影响，这是因为 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中在任何时间（以及在默认情况下）总是为数据库启用全文搜索。  
  
## <a name="corrective-action"></a>纠正措施  
 修改存储过程以删除这些属性。  
  
## <a name="see-also"></a>请参阅  
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  