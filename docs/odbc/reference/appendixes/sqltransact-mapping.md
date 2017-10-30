---
title: "SQLTransact 映射 |Microsoft 文档"
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
- mapping deprecated functions [ODBC], SQLTransact
- SQLTransact function [ODBC], mapping
ms.assetid: 8a01041f-3572-46f9-8213-b817f3cf929c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 252339f7fcd2a3893f030c0ffbc4485ab5441152
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqltransact-mapping"></a>SQLTransact 映射
**SQLTransact**现在已被取代通过**SQLEndTran**。 两个函数之间的主要区别在于**SQLEndTran**包含自变量*HandleType*，它指定要在完成工作的作用域。 *HandleType*自变量可以指定环境或连接句柄。 以下调用到**SQLTransact**:  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 映射到  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 如果*ConnectionHandle*是否不等于 SQL_NULL_HDBC。 *ConnectionHandle*参数设置的值为*hdbc*。  
  
 **SQL_Transact**映射到  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 如果*ConnectionHandle*等于 SQL_NULL_HDBC。 *EnvironmentHandle*参数设置的值为*henv*。  
  
 在这两个前面的情况下， *CompletionType*参数设置为相同的值*fType*。

