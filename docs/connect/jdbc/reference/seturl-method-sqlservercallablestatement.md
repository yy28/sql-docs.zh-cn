---
title: setURL 方法 (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3d83675e-74ca-49d9-8461-6326773c5c8c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d14c319da416990acd4dddc47843e7709895499b
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67972150"
---
# <a name="seturl-method-sqlservercallablestatement"></a>setURL 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的 URL 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setURL(java.lang.String sCol,  
                   java.net.URL u)  
```  
  
#### <a name="parameters"></a>parameters  
 sCol   
  
 一个字符串，该字符串包含参数的名称  。  
  
 *u*  
  
 URL 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setURL 方法由 java.sql.CallableStatement 接口中的 setURL 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
