---
title: "getNClob 方法 (int) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 10dfa251-9408-469e-ae2a-1acf3917cf47
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 071655069cbbd0548a513d2377f940467c040883
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="getnclob-method-int"></a>getNClob 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索的值指定 JDBC **NCLOB** Java 编程语言中的 NClob 对象作为参数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.NClob getNClob(int parameterIndex)  
```  
  
#### <a name="parameters"></a>Parameters  
 *parameterIndex*  
  
 **Int** ，该值指示参数索引。  
  
## <a name="return-value"></a>返回值  
 ANClobobject。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.CallableStatement 接口中的 getNClob 方法指定此 getNClob 方法。  
  
 此方法仅支持检索**NCHAR**， **NVARCHAR**， **NTEXT**，和**XML**参数。 在其他数据类型参数上调用这些方法会引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [getNClob 方法 &#40;SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
