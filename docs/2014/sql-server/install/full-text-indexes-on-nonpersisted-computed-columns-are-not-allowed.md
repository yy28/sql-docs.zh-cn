---
title: 不允许使用非持久化计算列上的全文索引 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 417ca3c2e5e477960c4c905543f3a712a5ec7453
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66095172"
---
# <a name="full-text-indexes-on-nonpersisted-computed-columns-are-not-allowed"></a>不允许对非持久化计算列建立全文检索
  不能对不确定的计算列和不精确的计算列创建全文检索。 此类列不能用作类型列或全文键列。  
  
## <a name="description"></a>Description  
 在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中，可以通过将不确定的计算列和不精确的计算列用作类型列或全文键列来创建全文检索。 现在不支持此功能。 当升级时，将禁用旧的、不兼容的和不支持的全文检索。  
  
## <a name="corrective-action"></a>纠正措施  
 若要启用这些全文检索，请修改相应的列定义，以使相应的列成为确定、精确的列。  
  
## <a name="see-also"></a>请参阅  
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
