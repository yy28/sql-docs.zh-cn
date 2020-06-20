---
title: 非持久化上的全文索引，不允许使用计算列 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes
ms.assetid: cba737f7-b187-47d0-8458-23dc18d18aca
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: de153d45e2f652bfea6e9dce68428af84be68b6c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012338"
---
# <a name="full-text-indexes-on-nonpersisted-computed-columns-are-not-allowed"></a>不允许对非持久化计算列建立全文检索
  不能对不确定的计算列和不精确的计算列创建全文检索。 此类列不能用作类型列或全文键列。  
  
## <a name="description"></a>说明  
 在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中，可以通过将不确定的计算列和不精确的计算列用作类型列或全文键列来创建全文检索。 现在不支持此功能。 当升级时，将禁用旧的、不兼容的和不支持的全文检索。  
  
## <a name="corrective-action"></a>纠正措施  
 若要启用这些全文检索，请修改相应的列定义，以使相应的列成为确定、精确的列。  
  
## <a name="see-also"></a>另请参阅  
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
