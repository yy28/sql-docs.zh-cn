---
title: ISQLServerCallableStatement 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 030a1631-cfcd-41e0-beb5-47f93c01e8e0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0a6d016f51dc5e651475cb5c6c58ed6cd0761b00
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47774636"
---
# <a name="isqlservercallablestatement-interface"></a>ISQLServerCallableStatement 接口
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示 JDBC 可调用语句。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 中新增了此接口。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **扩展：** java.sql.CallableStatement、[ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
public interface ISQLServerCallableStatement  
```  
  
## <a name="remarks"></a>Remarks  
 此接口由实现[SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)。  
  
 此接口公开以下 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 特定的方法：  
  
|方法|有关详细信息，请参阅|  
|------------|-------------------------------|  
|microsoft.sql.DateTimeOffset getDateTimeOffset(int)|[getDateTimeOffset(int)](../../../connect/jdbc/reference/getdatetimeoffset-method-int.md)|  
|microsoft.sql.DateTimeOffset getDateTimeOffset(String)|[getDateTimeOffset(String)](../../../connect/jdbc/reference/getdatetimeoffset-method-string.md)|  
|void setDateTimeOffset(String, microsoft.sql.DateTimeOffset)|[setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlservercallablestatement.md)|  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
