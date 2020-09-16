---
description: setTimestamp 方法 (java.lang.String, java.sql.Timestamp)
title: 设置时间戳值的 setTimestamp 方法 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setTimestamp (java.lang.String, java.sql.Timestamp)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dc45b126-3196-47ff-956b-cbc897980ff8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9f176b15ac48910cf4ce1de74a284fa5080cbc75
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450679"
---
# <a name="settimestamp-method-javalangstring-javasqltimestamp"></a>setTimestamp 方法 (java.lang.String, java.sql.Timestamp)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的时间戳值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setTimestamp(java.lang.String sCol,  
                         java.sql.Timestamp t)  
```  
  
#### <a name="parameters"></a>参数  
 sCol**  
  
 包含参数名称的字符串****。  
  
 *t*  
  
 Timestamp 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setTimestamp 方法是由 java.sql.CallableStatement 接口中的 setTimestamp 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [setTimestamp 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/settimestamp-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
