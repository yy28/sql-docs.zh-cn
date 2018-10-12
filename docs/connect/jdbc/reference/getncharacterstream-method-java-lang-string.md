---
title: getNCharacterStream 方法 (java.lang.String) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 45d2695b-0727-419d-8921-a51d6feef0aa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 994c4fa1b9c990afe98ebb272da32ef72c2f3544
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47769419"
---
# <a name="getncharacterstream-method-javalangstring"></a>getNCharacterStream 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  根据给定的参数名称，检索指定参数作为 Reader 对象的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final java.io.Reader getNCharacterStream(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>Parameters  
 *columnLabel*  
  
 一个包含列标签的 String。  
  
## <a name="return-value"></a>返回值  
 AReaderobject。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 访问时，应使用此方法**NCHAR**， **NVARCHAR**并**LONGNVARCHAR**参数。  
  
 此 getNCharacterStream 方法由 java.sql.CallableStatement 接口中的 getNCharacterStream 方法指定。  
  
## <a name="see-also"></a>另请参阅  
 [getNCharacterStream 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
