---
description: LIKE 谓词限制
title: LIKE 谓词限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- LIKE predicate limitations [ODBC]
- ODBC SQL grammar, LIKE predicate limitations
ms.assetid: dbd39099-caf6-4c4c-9ad8-f6c63c1bd5e4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 63410b78b6d0b7ab59dd74b9f69fe57fe498c6ea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483520"
---
# <a name="like-predicate-limitations"></a>LIKE 谓词限制
如果列中的数据长度超过255个字符，则 LIKE 比较将仅基于前255个字符。  
  
 在过程中使用的 LIKE 仅支持常量模式。 桌面数据库驱动程序支持 SQL-92，如模式匹配。  
  
 不支持在 LIKE 谓词中使用转义子句。  
  
 不应对包含 numeric 或 float 数据类型数据的列执行类似比较。 结果可能是不可预知的。 有关详细信息，请参阅 *Microsoft Jet 数据库引擎程序员指南*。
