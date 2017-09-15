---
title: "setNString 方法 (SQLServerCallableStatement) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6494300b-7fc0-4076-8311-22d35a96cdc6
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b7748fe8a19028542d76cda580f6bbb7c24f3a7a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setnstring-method-sqlservercallablestatement"></a>setNString 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定的参数设置为指定的字符串对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setNString(java.lang.String parameterName, java.lang.String value)  
```  
  
#### <a name="parameters"></a>Parameters  
 *参数名称*  
  
 A**字符串**，该值指示参数名称。  
  
 *值*  
  
 一个字符串对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 此方法应该用于**NCHAR**， **NVARCHAR**， **NTEXT**，和**XML**数据类型。  
  
 由 java.sql.CallableStatement 接口中的 setNString 方法指定此 setNString 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
