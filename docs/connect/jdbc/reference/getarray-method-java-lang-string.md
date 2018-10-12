---
title: getArray 方法 (java.lang.String) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getArray (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4610cbaf-5638-4a66-bd83-70aefca40e58
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eefc1d5c3f71618fc448b27c5c91cdb82b12e7b1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47778375"
---
# <a name="getarray-method-javalangstring"></a>getArray 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数名称检索指定参数作为 Array 对象的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Array getArray(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parameters  
 *sCol*  
  
 包含参数名称的字符串。  
  
## <a name="return-value"></a>返回值  
 一个数组对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getArray 方法是由 java.sql.CallableStatement 接口中的 getArray 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [getArray 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getarray-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
