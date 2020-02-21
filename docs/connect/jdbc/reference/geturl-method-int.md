---
title: getURL 方法 (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getURL Ijnt)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 75d03ced-3614-4997-9abd-24642b1d1aae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b7b91071c97c46d7516907459539303ddbd45822
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67978329"
---
# <a name="geturl-method-int"></a>getURL 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数索引检索指定参数作为 Java 编程语言中的 URL 对象的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.net.URL getURL(int n)  
```  
  
#### <a name="parameters"></a>parameters  
 *n*  
  
 指示参数索引的 int  。  
  
## <a name="return-value"></a>返回值  
 URL 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getURL 方法是由 java.sql.CallableStatement 接口中的 getURL 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [getURL 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/geturl-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
