---
title: "孙聚合 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- grandchild aggregates [ADO]
- data shaping [ADO], grandchild aggregates
ms.assetid: 4162d35f-2ce1-4218-80a5-b6933348837e
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8889be6c78765d7eadf211016de92d041c9419f3
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="grandchild-aggregates"></a>孙聚合
创建形状命令的子句中的章节列中可能会获得*章别名*（通常使用 AS 关键字）。 你可以标识任何章节中的形状的任何列**记录集**标识包含此列的子级的完全限定名称。 例如，如果父章，chap1，包含子章节，chap2，具有量列中，amt，则的限定的名称将为 chap1.chap2.amt。随后可作为一个聚合函数 （SUM、 AVG、 最大值、 最小值、 计数、 STDEV、 或任何） 的自变量的限定的名称。  
  
## <a name="see-also"></a>另请参阅  
 [数据整理示例](../../../ado/guide/data/data-shaping-example.md)
