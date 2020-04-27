---
title: 对字符串长度和子字符串的行为的更改 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2119b7ba-2e52-44bf-ac57-82c2d46a48ff
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 18643dfc11d2b1b1d875a19c478f9ec8cbdd5be6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66428844"
---
# <a name="changes-to-behavior-of-string-length-and-substring"></a>string-length 和 substring 行为的变化
  当与包含代理项字符的 XML 数据库一起使用时，[字符串长度函数 &#40;xquery&#41;](/sql/xquery/functions-on-string-values-string-length)和[Substring 函数 &#40;xquery&#41;](/sql/xquery/functions-on-string-values-substring)函数可能返回不同的结果。  
  
## <a name="description"></a>说明  
 如果数据库设置为与[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]兼容，则在处理 Unicode 补充字符的情况下，[字符串长度函数 &#40;xquery&#41;](/sql/xquery/functions-on-string-values-string-length)和[substring 函数 &#40;xquery&#41;](/sql/xquery/functions-on-string-values-substring)函数更改。 每个 Unicode 增补字符（通过大于 U+FFFF 的码位来定义）将被这些函数计为一个字符，而不是早期版本中的两个字符。  
  
 有关代理项字符的详细信息，请参阅[代理项和补充字符](https://go.microsoft.com/fwlink/?LinkId=178317)。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](https://docs.microsoft.com/sql/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
