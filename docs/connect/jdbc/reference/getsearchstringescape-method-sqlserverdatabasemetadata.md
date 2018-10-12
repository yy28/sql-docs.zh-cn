---
title: getSearchStringEscape 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSearchStringEscape
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ea0f95d0-0238-4dc8-9f26-7ff9b65f30c3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1a12b9ca70dd8e48fa92df9b1b2be55b22ee6994
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47721355"
---
# <a name="getsearchstringescape-method-sqlserverdatabasemetadata"></a>getSearchStringEscape 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索可用于转义通配符的 String 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getSearchStringEscape()  
```  
  
## <a name="return-value"></a>返回值  
 包含转义通配符字符串的 String。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getSearchStringEscape 方法由 java.sql.DatabaseMetaData 接口中的 getSearchStringEscape 方法指定。  
  
 此方法仅用于元数据模式搜索。 它返回“\\”。 String 搜索模式可以对通配符（“%”和“_”）进行转义，并通过在这些通配符之前加反斜杠将其作为文字提供。 这样可将“\\%”转换为“[%]”，将“\\\_”转换为“[\_]”。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
