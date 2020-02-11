---
title: 修改使用了不再使用的全文搜索属性的存储过程 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- discontinued properties [Full-Text Search]
- stored procedures [Full-Text Search]
ms.assetid: 8d9392d9-a9ba-4378-84e4-59f516b67ddb
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5204b27fb4745f8005a328dc62503f7db418387d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093853"
---
# <a name="modify-stored-procedures-that-use-discontinued-full-text-search-properties"></a>修改使用已停用全文搜索属性的存储过程
  为确保存储过程正确执行，应编辑现有过程并删除已删除或已废弃的与全文相关的属性和设置。  
  
## <a name="component"></a>组件  
 全文搜索  
  
## <a name="description"></a>说明  
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
  
## <a name="see-also"></a>另请参阅  
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
