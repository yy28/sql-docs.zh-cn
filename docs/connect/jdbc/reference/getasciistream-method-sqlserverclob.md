---
title: getAsciiStream 方法 (SQLServerClob) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.getAsciiStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 134abe5e-5add-4d27-b333-b4b0f4d94c31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2490fc903f7c1c509adc1e6f776f00a39e5f4616
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47767265"
---
# <a name="getasciistream-method-sqlserverclob"></a>getAsciiStream 方法 (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将 CLOB 作为 ASCII 流具体化。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.io.InputStream getAsciiStream()  
```  
  
## <a name="return-value"></a>返回值  
 包含 CLOB 数据的输入流。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getAsciiStream 方法由 java.sql.Clob 接口中的 getAsciiStream 方法指定。  
  
 始终返回字节流并假定 CLOB 中的数据采用 ASCII 格式，因为系统无法知道它是 Unicode 还是任何其他多字节代码页。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerClob 方法](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 成员](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 类](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
