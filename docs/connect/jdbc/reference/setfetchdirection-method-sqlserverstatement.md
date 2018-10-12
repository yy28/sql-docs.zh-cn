---
title: setFetchDirection 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 18176517-2fb3-4266-924d-0f01253083d2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f3c6e0080f4d94b0d792c1994695c590fd4fed66
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812335"
---
# <a name="setfetchdirection-method-sqlserverstatement"></a>setFetchDirection 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  为 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 提供提示以指明处理结果集行时应采用的方向。  
  
> [!NOTE]  
>  JDBC 驱动程序目前忽略了此方法给出的提示。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setFetchDirection(int nDir)  
```  
  
#### <a name="parameters"></a>Parameters  
 *nDir*  
  
 指示行处理方向的 int，可以为以下值之一：  
  
 FETCH_FORWARD  
  
 FETCH_REVERSE  
  
 FETCH_UNKNOWN  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setFetchDirection 方法由 java.sql.Statement 接口中的 setFetchDirection 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
