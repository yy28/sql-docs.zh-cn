---
title: getParameterMode 方法 (SQLServerParameterMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.getParameterMode
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d93c9b70-18c2-44bb-a6de-70a7e940d806
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3d5c9c03946082f9af3f939c44d13c350bd9b403
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47647644"
---
# <a name="getparametermode-method-sqlserverparametermetadata"></a>getParameterMode 方法 (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索指定参数的模式。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getParameterMode(int param)  
```  
  
#### <a name="parameters"></a>Parameters  
 *param*  
  
 指示参数索引的 int。  
  
## <a name="return-value"></a>返回值  
 指示指定参数的模式的 int，可以为以下值之一：  
  
 ParameterMetaData.parameterModeIn  
  
 ParameterMetaData.parameterModeInOut  
  
 ParameterMetaData.parameterModeOut  
  
 ParameterMetaData.parameterModeUnknown  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getParameterMode 方法指定 java.sql.ParameterMetaData 接口中的 getParameterMode 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerParameterMetaData 方法](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 成员](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 类](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
