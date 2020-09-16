---
description: setNull 方法 (java.lang.String, int)
title: setNull 方法 (java.lang.String, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setNull (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e1d7e267-d9de-407a-b1a9-abdc2623478d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2fca7e30e3aa3f66f76d4877ea250a66fc7af632
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458609"
---
# <a name="setnull-method-javalangstring-int"></a>setNull 方法 (java.lang.String, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据要设置的参数的类型，将指定参数设置为 Null 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setNull(java.lang.String sCol,  
                    int nType)  
```  
  
#### <a name="parameters"></a>参数  
 sCol**  
  
 包含参数名称的字符串****。  
  
 nType**  
  
 由 java.sql.Types 定义的 JDBC 类型代码。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setNull 方法由 java.sql.CallableStatement 接口中的 setNull 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [setNull 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setnull-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
