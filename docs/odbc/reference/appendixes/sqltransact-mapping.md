---
title: SQLTransact 映射 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLTransact
- SQLTransact function [ODBC], mapping
ms.assetid: 8a01041f-3572-46f9-8213-b817f3cf929c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6aaa056fca860a70f81ad7c3a4cd8539512bc25d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304878"
---
# <a name="sqltransact-mapping"></a>SQLTransact 映射
**SQLTransact**现在被**SQLEndTran**替换。 这两个函数之间的主要区别是**SQLEndTran**包含一个参数*HandleType，* 它指定要完成的工作范围。 *HandleType*参数可以指定环境或连接句柄。 以下调用**SQLTransact**：  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 映射到  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 如果*连接句柄*不等于SQL_NULL_HDBC。 *ConnectHandle*参数设置为*hdbc*的值。  
  
 **SQL_Transact**映射到  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 如果*连接句柄*等于SQL_NULL_HDBC。 *环境句柄*参数设置为*henv*的值。  
  
 在前面的两种情况下，*完成类型*参数设置为与*fType*相同的值。
