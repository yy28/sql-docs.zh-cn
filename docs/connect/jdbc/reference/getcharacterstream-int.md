---
title: getCharacterStream (int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getCharacterStream(int paramIndex)
apilocation:
- SQLServerCallableStatement.getCharacterStream(int paramIndex)
apitype: Assembly
ms.assetid: eb20714b-52bc-4b6c-b23f-c9c3c9d73783
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f72510a01362dfea3772e5ccbe4ea5ec47ccf41f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802118"
---
# <a name="getcharacterstream-int"></a>getCharacterStream (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数索引检索指定参数的值作为 java.io.Reader 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final java.io.Reader getCharacterStream(int paramIndex)  
```  
  
#### <a name="parameters"></a>Parameters  
 paramIndex   
  
 指示参数索引的 int  。  
  
## <a name="return-value"></a>返回值  
 Reader 对象。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>另请参阅  
 [getCharacterStream 方法 (SQLServerCallableStatement)](../../../connect/jdbc/reference/getcharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
