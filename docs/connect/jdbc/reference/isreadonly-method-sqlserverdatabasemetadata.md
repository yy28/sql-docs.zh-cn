---
title: isReadOnly 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.isReadOnly
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d1569e03-b7bd-486a-af0b-d3f108f712dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f27d80ab24b03422aea8e96ad3a046f449e05a2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47782825"
---
# <a name="isreadonly-method-sqlserverdatabasemetadata"></a>isReadOnly 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索此数据库是否处于只读模式。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean isReadOnly()  
```  
  
## <a name="return-value"></a>返回值  
 如果数据库处于只读模式，则为 true。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 isReadOnly 方法由 java.sql.DatabaseMetaData 接口中的 isReadOnly 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
