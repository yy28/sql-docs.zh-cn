---
title: getCharacterStream 方法 () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.getCharacterStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 70a5a8c8-791a-43f9-8a0e-1c390f30857c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e9cacf116a8da7db6651bd000c14329b3e62a0c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67953190"
---
# <a name="getcharacterstream-method-"></a>getCharacterStream 方法 ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将 CLOB  数据作为 Reader 对象或字符流返回。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.io.Reader getCharacterStream()  
```  
  
## <a name="return-value"></a>返回值  
 包含 CLOB  数据的 Reader 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getCharacterStream 方法是由 java.sql.Clob 接口中的 getCharacterStream 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerClob 方法](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 成员](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 类](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
