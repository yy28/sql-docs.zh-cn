---
description: 标识符限制
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f5efaba8fa73f61082be8d7cd8dca78626a9f972
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500340"
---
# <a name="identifiers-limitations"></a>标识符限制
如果标识符包含空格或特殊符号，则该标识符必须用后引号括起来。 有效名称是不超过64个字符的字符串，其中第一个字符不得为空格。 有效名称不能包含控制字符或以下特殊字符： ' &#124; # *？ [ ] . ! $ .  
  
 不要使用 *ODBC 程序员参考* (附录 C 中的 SQL 语法中所列的保留字，也不要使用这些保留字的简写形式) 作为标识符 (也就是说，表名或列名) ，除非将单词括在引号 (") 中。
