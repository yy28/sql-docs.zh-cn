---
description: 孙级聚合
title: 孙聚合 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7215846215db30d31d9a7b54f8e3a3aa2a955a43
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806799"
---
# <a name="grandchild-aggregates"></a>孙级聚合
可以为 shape 命令的子句中创建的章节列指定 *章节别名* ， (通常使用 AS 关键字) 。 您可以使用标识包含列的子级的完全限定名称标识整形 **记录集** 的任何章节中的任何列。 例如，如果父章节 chap1 包含一个 chap2，其中包含一个 "金额" 列，则该限定名称为 "chap1"。限定名称随后可用作聚合函数之一的参数 (SUM、AVG、MAX、MIN、COUNT、STDEV 或 ANY) 。  
  
## <a name="see-also"></a>另请参阅  
 [数据整理示例](./data-shaping-example.md)