---
description: SQLTransact 映射
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cf1298c9881a207c21074e03e8b0597ab8f11448
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429498"
---
# <a name="sqltransact-mapping"></a>SQLTransact 映射
**SQLTransact** 现已替换为 **SQLEndTran**。 这两个函数之间的主要区别在于， **SQLEndTran** 包含一个参数 *HandleType*，该参数指定要完成的工作的范围。 *HandleType*参数可指定环境或连接句柄。 对 **SQLTransact**的以下调用：  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 映射到  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 如果 *ConnectionHandle* 不等于 SQL_NULL_HDBC。 *ConnectionHandle*参数设置为*hdbc*的值。  
  
 **SQL_Transact** 映射到  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 如果 *ConnectionHandle* 等于 SQL_NULL_HDBC。 *EnvironmentHandle*参数设置为*henv*的值。  
  
 在上述两种情况下， *CompletionType* 参数将设置为与 *fType*相同的值。
