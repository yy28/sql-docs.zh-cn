---
title: LIKE 转义序列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 517c21f7b64fa7ceb662af9839a9fed1a1e6eff6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304918"
---
# <a name="like-escape-sequence"></a>LIKE 转义序列
ODBC 对 LIKE 子句使用转义序列。 此转义序列的语法如下所示：  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>备注  
 在 BNF 表示法中，语法如下：  
  
 *类似 ODBC-escape* ：： =  
  
 *Odbc-esc-发起程序*转义符 \*转义*符 ' *odbc-esc-终止符*  
  
 *转义*符：： =*字符*  
  
 *ODBC-esc-发起方*：： = {  
  
 *ODBC-esc-终止符*：： =}  
  
 若要确定驱动程序是否支持类似的转义序列，应用程序可以使用 SQL_LIKE_ESCAPE_CLAUSE 信息类型调用**SQLGetInfo** 。
