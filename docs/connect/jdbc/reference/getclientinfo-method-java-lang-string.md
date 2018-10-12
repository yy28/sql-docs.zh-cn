---
title: getClientInfo 方法 (java.lang.String) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e8e632c4-d6cc-4c5e-b6ad-873579343b19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eb792035b5926d94654dec3a445599165cd5fbdf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47645805"
---
# <a name="getclientinfo-method-javalangstring"></a>getClientInfo 方法 (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索指定客户端信息属性的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getClientInfo (java.lang.String name)  
```  
  
#### <a name="parameters"></a>Parameters  
 *名称*  
  
 包含要检索的客户端信息属性名称的 String。  
  
## <a name="return-value"></a>返回值  
 包含客户端信息属性值的 String。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getClientInfo 方法由 java.sql.Connection 接口中的 getClientInfo 方法指定。  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 不支持任何客户端信息属性。 因此，此方法将返回 null。  
  
 与此类似，应用程序可以使用 [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) 类中的 [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) 方法来检索驱动程序支持的客户端信息属性列表。 [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) 方法返回空结果集。  
  
## <a name="see-also"></a>另请参阅  
 [getClientInfo 方法 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection 成员](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 类](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
