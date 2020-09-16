---
description: getBlob 方法 (java.lang.String)
title: getBlob 方法 (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBlob (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3fe74b50-9ccd-4973-a93a-6da2c20a4154
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a3b9772e084bb8c98fe67977e4a49b3375f8f025
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437119"
---
# <a name="getblob-method-javalangstring"></a>getBlob 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数名称，检索指定 JDBC BLOB 参数作为 Java 编程语言中的 BLOB 对象的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Blob getBlob(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>参数  
 sCol**  
  
 包含参数名称的字符串****。  
  
## <a name="return-value"></a>返回值  
 Blob 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getBlob 方法是由 java.sql.CallableStatement 接口中的 getBlob 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [getBlob 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getblob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
