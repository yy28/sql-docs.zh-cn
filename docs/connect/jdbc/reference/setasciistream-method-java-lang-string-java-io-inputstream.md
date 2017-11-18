---
title: "setAsciiStream 方法输入流 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dc2caa44-9eb5-4ed8-a889-36148b50901d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4b856948b2e8e50613dc08d7482be6b242d40318
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setasciistream-method-javalangstring-javaioinputstream"></a>setAsciiStream 方法 (java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为指定的输入流。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setAsciiStream(java.lang.String parameterName,  
                                java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parameters  
 *参数名称*  
  
 A**字符串**，其中包含参数名称。  
  
 *x*  
  
 一个 InputStream 对象中。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.PreparedStatement 接口中的 setAsciiStream 方法指定此 setAsciiStream 方法。  
  
## <a name="see-also"></a>另请参阅  
 [setAsciiStream &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/setasciistream-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  

