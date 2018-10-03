---
title: 标识符限制 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c781113124d456e1ba866546d6ada7a17371d71f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47667385"
---
# <a name="identifiers-limitations"></a>标识符限制
如果标识符包含空格或特殊符号后, 引号必须用标识符。 有效的名称是不能超过 64 个字符，其中第一个字符必须不能有空格的字符串。 有效的名称不能包含控制字符或下列特殊字符: &#124; # *？ [ ] . ! $ .  
  
 请不要的使用保留的字中的附录 C 中的 SQL 语法列出*ODBC 程序员参考*（或这些保留字的简写形式） 作为标识符 （即，表或列名称），除非环绕 word 后退单引号 （'））。
