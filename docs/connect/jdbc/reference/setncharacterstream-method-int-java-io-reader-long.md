---
title: setNCharacterStream 方法到 java.io.Reader 对象-长 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36396dc9-f109-4da0-bd64-726704046bbf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3d32bdf91cfe9ddbbdc8e3bb85e101943aebcf4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47736265"
---
# <a name="setncharacterstream-method-int-javaioreader-long"></a>setNCharacterStream 方法 (int, java.io.Reader, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为指定的 Reader 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setNCharacterStream(int parameterIndex,  
                                                  java.io.Reader value,  
                                                                long length)  
```  
  
#### <a name="parameters"></a>Parameters  
 *parameterIndex*  
  
 指示参数索引的 int。  
  
 *value*  
  
 包含参数值的 Reader 对象。  
  
 *length*  
  
 指示参数值中字符数的 long。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 setNCharacterStream 方法由 java.sql.PreparedStatement 接口中的 setNCharacterStream 方法指定。  
  
 此方法应用于**NCHAR**， **NVARCHAR**， **NTEXT**，以及**XML**数据类型。  
  
 如果流长度与 length 参数指定的长度不同，则 JDBC 驱动程序将在更新或插入行时引发异常。  
  
 如果流长度未知，则可将 length 参数设置为 -1 以指示驱动程序应接受流而不考虑其长度。 使用 sqljdbc4.jar，当应用程序希望使用长度未知的流来更新列时，建议使用 JDBC 4.0 方法 [setNCharacterStream 方法 &#40;int, java.io.Reader&#41;](../../../connect/jdbc/reference/setncharacterstream-method-int-java-io-reader.md)。  
  
## <a name="see-also"></a>另请参阅  
 [setNCharacterStream 方法 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 成员](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
