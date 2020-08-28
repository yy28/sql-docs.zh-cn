---
description: 中间 Shape COMPUTE 子句
title: 干预形状计算子句 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- COMPUTE clause [ADO]
- data shaping [ADO], COMPUTE clause
ms.assetid: a576bf81-8f3c-4ba1-817b-87e89a8da684
author: rothja
ms.author: jroth
ms.openlocfilehash: 8a4be3fb7f70ba41e24cd757da34e7272e51f87c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980438"
---
# <a name="intervening-shape-compute-clauses"></a>中间 Shape COMPUTE 子句
将一个或多个 COMPUTE 子句嵌入到参数化形状命令中的父和子命令中是有效的，如以下示例中所示：  
  
```  
SHAPE {select au_lname, state from authors} APPEND   
   ((SHAPE   
      (SHAPE   
         {select * from authors where state = ?} rs   
      COMPUTE rs, ANY(rs.state) state, ANY(rs.au_lname) au_lname   
      BY au_id) rs2   
   COMPUTE rs2, ANY(rs2.state) BY au_lname)   
RELATE state TO PARAMETER 0)  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据定形示例](./data-shaping-example.md)   
 [正式形状语法](./formal-shape-grammar.md)   
 [常用 Shape 命令](./shape-commands-in-general.md)