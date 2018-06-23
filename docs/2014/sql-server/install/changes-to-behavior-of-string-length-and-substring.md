---
title: 字符串长度和子字符串行为的更改 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2119b7ba-2e52-44bf-ac57-82c2d46a48ff
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3bdc5e23a18b1b182703a1773dc8476eda8d4b14
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125059"
---
# <a name="changes-to-behavior-of-string-length-and-substring"></a>string-length 和 substring 行为的变化
  [字符串长度函数&#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-string-length)和[substring 函数&#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-substring)函数可能会返回不同的结果与包含的 XML 数据库一起使用时代理项字符。  
  
## <a name="description"></a>Description  
 当数据库设置为与兼容[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]的行为[字符串长度函数&#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-string-length)和[substring 函数&#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-substring)在处理 Unicode 补充字符的功能更改。 每个 Unicode 增补字符（通过大于 U+FFFF 的码位来定义）将被这些函数计为一个字符，而不是早期版本中的两个字符。  
  
 有关代理项字符的详细信息，请参阅[代理项和增补字符](http://go.microsoft.com/fwlink/?LinkId=178317)。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
