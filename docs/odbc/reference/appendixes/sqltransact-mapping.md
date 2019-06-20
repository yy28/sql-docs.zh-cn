---
title: SQLTransact 映射 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d5cf669883ce81528adbe1fbd8faeff2ed716218
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62735131"
---
# <a name="sqltransact-mapping"></a>SQLTransact 映射
**SQLTransact**现被替代**SQLEndTran**。 两个函数之间的主要区别在于**SQLEndTran**包含的参数*HandleType*，它指定要完成工作的范围。 *HandleType*参数可指定环境的信息或连接句柄。 以下调用到**SQLTransact**:  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 映射到  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 如果*ConnectionHandle*不等于 SQL_NULL_HDBC。 *ConnectionHandle*参数设置的值为*hdbc*。  
  
 **SQL_Transact**映射到  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 如果*ConnectionHandle*等于 SQL_NULL_HDBC。 *EnvironmentHandle*参数设置的值为*henv*。  
  
 在这种上述情况下， *CompletionType*参数设置为相同的值*fType*。
