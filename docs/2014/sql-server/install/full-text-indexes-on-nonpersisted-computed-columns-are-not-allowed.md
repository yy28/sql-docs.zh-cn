---
title: 不允许持久化计算列上的全文索引 |Microsoft 文档
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
- full-text indexes
ms.assetid: cba737f7-b187-47d0-8458-23dc18d18aca
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d51500dca40ed039816b973cb4698971996e2b01
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125053"
---
# <a name="full-text-indexes-on-nonpersisted-computed-columns-are-not-allowed"></a>不允许对非持久化计算列建立全文检索
  不能对不确定的计算列和不精确的计算列创建全文检索。 此类列不能用作类型列或全文键列。  
  
## <a name="description"></a>Description  
 在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中，可以通过将不确定的计算列和不精确的计算列用作类型列或全文键列来创建全文检索。 现在不支持此功能。 当升级时，将禁用旧的、不兼容的和不支持的全文检索。  
  
## <a name="corrective-action"></a>纠正措施  
 若要启用这些全文检索，请修改相应的列定义，以使相应的列成为确定、精确的列。  
  
## <a name="see-also"></a>请参阅  
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  