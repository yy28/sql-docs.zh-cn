---
title: createClob 方法 (SQLServerConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 58b0865a-1cde-4046-9761-51e471294023
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: add9cb59748ce4de615ec4ac73117984bb2c8642
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66795566"
---
# <a name="createclob-method-sqlserverconnection"></a>createClob 方法 (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  创建不包含任何数据的 Clob 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.sql.Clob createClob()  
```  
  
## <a name="return-value"></a>返回值  
 Clob 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 createClob 方法由 java.sql.Connection 接口中的 createClob 方法指定。  
  
 此方法无需[SQLServerClob 构造函数&#40;SQLServerConnection，java.lang.String&#41;](../../../connect/jdbc/reference/sqlserverclob-constructor-sqlserverconnection-java-lang-string.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
