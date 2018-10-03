---
title: 孙级聚合 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- grandchild aggregates [ADO]
- data shaping [ADO], grandchild aggregates
ms.assetid: 4162d35f-2ce1-4218-80a5-b6933348837e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1bff3c8a155e1e9378acbb659f00817f478382e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47602375"
---
# <a name="grandchild-aggregates"></a>孙级聚合
创建的形状命令子句中的章节列中可能会获得*章别名*（通常使用 AS 关键字）。 可以识别的形状的任何一章中的任何列**记录集**与标识包含的列的子级的完全限定名称。 例如，如果父一章，chap1，包含子章节，chap2，具有一个 amount 列，amt 设置，则限定的名称将为 chap1.chap2.amt。然后可以作为一个聚合函数 （SUM、 AVG、 最大值、 最小值、 计数、 STDEV、 或任意） 的参数使用的限定的名称。  
  
## <a name="see-also"></a>请参阅  
 [数据整理示例](../../../ado/guide/data/data-shaping-example.md)
