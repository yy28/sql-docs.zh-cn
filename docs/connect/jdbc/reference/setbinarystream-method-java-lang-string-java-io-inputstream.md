---
title: setBinaryStream 方法的输入流) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 339c8277-2d08-4094-9fa9-26c8ad3e7348
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 67b7b7ae7e9e90bab4ad22cbebf248b62351749b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47766777"
---
# <a name="setbinarystream-method-javalangstring-javaioinputstream"></a>setBinaryStream 方法 (java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为指定的输入流。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setBinaryStream(java.lang.String parameterName,  
                            java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parameters  
 parameterName  
  
 一个字符串，该字符串包含参数的名称。  
  
 *x*  
  
 InputStream 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setBinaryStream 方法由 java.sql.CallableStatement 接口中的 setBinaryStream 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [setBinaryStream (SQLServerCallableStatement)](../../../connect/jdbc/reference/setbinarystream-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
