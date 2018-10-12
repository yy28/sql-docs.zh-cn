---
title: getCharacterStream 方法 （) (SQLServerNClob) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7641698e-b25c-4bb2-bcc7-9273bdd08bf0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4cf25f858e740dcb8ec9d10467808bcd619aec46
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47801775"
---
# <a name="getcharacterstream-method--sqlservernclob"></a>getCharacterStream 方法 () (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索**NCLOB**数据作为**读取器**对象或字符流。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.io.Reader getCharacterStream()  
```  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="return-value"></a>返回值  
 包含 NCLOB 数据的 Reader 对象。  
  
## <a name="remarks"></a>Remarks  
 此 getCharacterStream 方法由 java.sql.NClob 接口中的 getCharacterStream 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [getCharacterStream 方法 &#40;SQLServerNClob&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)   
 [SQLServerNClob 方法](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob 成员](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob 类](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
