---
title: getGeneratedKeys 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getGeneratedKeys
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a3325950-0e81-4ae8-aa0c-e1f6d371adcd
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e81fe589ed70f4d3f230713290f1d7f9b338ea67
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66774653"
---
# <a name="getgeneratedkeys-method-sqlserverstatement"></a>getGeneratedKeys 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索因运行此 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象而创建的任何自动生成的键。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final java.sql.ResultSet getGeneratedKeys()  
```  
  
## <a name="return-value"></a>返回值  
 一个结果集的对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getGeneratedKeys 方法由 java.sql.Statement 接口中的 getGeneratedKeys 方法指定。  
  
 有关如何使用此方法的详细信息，请参阅[使用自动生成的键](../../../connect/jdbc/using-auto-generated-keys.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
