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
ms.openlocfilehash: 251ae0e4e94cec903e2c4b5cf687ed9b8b41dfc8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67952392"
---
# <a name="identifiers-limitations"></a>标识符限制
如果标识符包含空格或特殊符号，则该标识符必须用后引号括起来。 有效名称是不超过64个字符的字符串，其中第一个字符不得为空格。 有效名称不能包含控制字符或以下特殊字符： ' &#124; # *？ [ ] . ! $ .  
  
 不要使用*ODBC 程序员参考*的附录 C （或这些保留字的简写形式）的 SQL 语法中列出的保留字作为标识符（即表名或列名），除非你将单词括在后面的引号（'）中。
