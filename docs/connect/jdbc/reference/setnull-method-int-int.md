---
title: setNull 方法 （int，int） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setNull (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7e7f08e9-278a-495a-8ce3-ca173d055021
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 977ca2ec68888bfc53ca1256da97f1bf427c33f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66800318"
---
# <a name="setnull-method-int-int"></a>setNull 方法 (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据要设置的参数的类型，将指定参数设置为 Null 值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setNull(int index,  
                          int jdbcType)  
```  
  
#### <a name="parameters"></a>Parameters  
 索引   
  
 指示参数编号的 int  。  
  
 jdbcType   
  
 由 java.sql.Types 定义的 JDBC 类型代码。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setNull 方法是由 java.sql.PreparedStatement 接口中的 setNull 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [setNull 方法 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setnull-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 类](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
