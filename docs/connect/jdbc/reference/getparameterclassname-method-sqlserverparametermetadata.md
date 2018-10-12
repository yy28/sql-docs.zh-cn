---
title: getParameterClassName 方法 (SQLServerParameterMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.getParameterClassName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 545634d8-f06b-429a-9293-0087d758f359
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fcbcac8f48c47f2144127ecd2aa41a5402bf6f38
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47818159"
---
# <a name="getparameterclassname-method-sqlserverparametermetadata"></a>getParameterClassName 方法 (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索指定 Java 类的完全限定名称，而该 Java 类的实例应传递给 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 类中的 [setObject](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) 方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getParameterClassName(int param)  
```  
  
#### <a name="parameters"></a>Parameters  
 *param*  
  
 指示参数索引的 int。  
  
## <a name="return-value"></a>返回值  
 包含完全限定类名称的 String。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getParameterClassName 方法指定 java.sql.ParameterMetaData 接口中的 getParameterClassName 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerParameterMetaData 方法](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 成员](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 类](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
