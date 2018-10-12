---
title: getNClob 方法 (int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 10dfa251-9408-469e-ae2a-1acf3917cf47
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d55e65eba2f83f1ba8ae65ff110e2456958a719
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812347"
---
# <a name="getnclob-method-int"></a>getNClob 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索指定 JDBC NCLOB 参数作为 Java 编程语言中的 NClob 对象的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.NClob getNClob(int parameterIndex)  
```  
  
#### <a name="parameters"></a>Parameters  
 *parameterIndex*  
  
 指示参数索引的 int。  
  
## <a name="return-value"></a>返回值  
 ANClobobject。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getNClob 方法是由 java.sql.CallableStatement 接口中的 getNClob 方法指定的。  
  
 此方法仅支持检索**NCHAR**， **NVARCHAR**， **NTEXT**，以及**XML**参数。 在其他数据类型参数上调用这些方法会引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [getNClob 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
