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
ms.openlocfilehash: b2082a97b24284afcc879048bb08e86a7b2bb3ba
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070113"
---
# <a name="sqltransact-mapping"></a>SQLTransact 映射
**SQLTransact**现已替换为**SQLEndTran**。 这两个函数之间的主要区别在于， **SQLEndTran**包含一个参数*HandleType*，该参数指定要完成的工作的范围。 *HandleType*参数可指定环境或连接句柄。 对**SQLTransact**的以下调用：  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 映射到  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 如果*ConnectionHandle*不等于 SQL_NULL_HDBC。 *ConnectionHandle*参数设置为*hdbc*的值。  
  
 **SQL_Transact**映射到  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 如果*ConnectionHandle*等于 SQL_NULL_HDBC。 *EnvironmentHandle*参数设置为*henv*的值。  
  
 在上述两种情况下， *CompletionType*参数将设置为与*fType*相同的值。
