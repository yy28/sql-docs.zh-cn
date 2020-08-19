---
description: 混合命令
title: 混合命令 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- hybrid commands [ADO]
- data shaping [ADO], hybrid commands
ms.assetid: e8ca40e8-459c-40e2-8dd3-3ec6d5ee7b51
author: rothja
ms.author: jroth
ms.openlocfilehash: d3c6a852f5918a79c0fb2df5e2f60ef415cca6a1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453239"
---
# <a name="hybrid-commands"></a>混合命令
混合命令是部分参数化命令。 例如：  
  
```  
SHAPE {select * from plants}   
   APPEND( {select * from customers where country = ?}   
           RELATE PlantCountry TO PARAMETER 0,   
             PlantRegion TO CustomerRegion )   
```  
  
 混合命令的缓存行为与常规参数化命令的行为相同。  
  
## <a name="see-also"></a>另请参阅  
 [数据定形示例](../../../ado/guide/data/data-shaping-example.md)   
 [正式形状语法](../../../ado/guide/data/formal-shape-grammar.md)   
 [常用 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
