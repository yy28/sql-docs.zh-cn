---
title: 标识符限制 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: b3466382-71cb-4f82-8318-092a8fcef3df
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 087d7ba056a5da10ae8d191592f06c312583b62b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="identifiers-limitations"></a>标识符限制
如果标识符包含空格或特殊符号，该标识符必须用后引号引起来。 有效的名称是不能超过 64 个字符，其中的第一个字符必须不能有空格的字符串。 有效的名称不能包含控制字符或以下特殊字符: &#124; # *？ [ ] . ! $ .  
  
 请不要的使用保留的字中的附录 C 中的 SQL 语法列出*ODBC 程序员参考*（或速记形式这些保留字） 作为标识符 （即，表或列名称），除非括住在返回的单词引号 （'）。
