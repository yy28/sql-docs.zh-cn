---
title: 标识符限制 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: b3466382-71cb-4f82-8318-092a8fcef3df
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7154f2db09b69e6376b1fe3af1de3f2c646ee94e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286247"
---
# <a name="identifiers-limitations"></a>标识符限制
如果标识符包含空格或特殊符号，则必须在后引号中包含标识符。 有效名称是不超过 64 个字符的字符串，其中第一个字符不能是空格。 有效名称不能包括控制字符或以下特殊字符："&#124; = * ？ [ ] . ! $ .  
  
 请勿使用*ODBC 程序员参考*附录 C 附录 C 中列出的保留词（或这些保留词的速记形式）作为标识符（即表或列名称），除非您在后引号 （'） 中环绕该单词。
