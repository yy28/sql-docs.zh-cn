---
title: "如转义序列 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 678f2f8f720823ef5658ba7ee1e1391bbebc1c50
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="like-escape-sequence"></a>如转义序列
ODBC 为 LIKE 子句使用转义序列。 此转义序列的语法如下所示：  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>注释  
 BNF 表示法中的语法，如下所示是：  
  
 *ODBC 类似转义*:: =  
  
 *ODBC esc 启动器*转义*转义符* *ODBC esc 终止符*  
  
 *转义字符*:: =*字符*  
  
 *ODBC esc 启动器*:: = {  
  
 *ODBC esc 终止符*:: =}  
  
 若要确定驱动程序是否支持 LIKE 转义序列，应用程序可以调用**SQLGetInfo** SQL_LIKE_ESCAPE_CLAUSE 信息类型。

