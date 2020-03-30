---
title: getParameterClassName 方法 (SQLServerParameterMetaData) | Microsoft Docs
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
ms.openlocfilehash: e0c5018dc2058af72028a4114dcc896d06d212d5
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67981009"
---
# <a name="getparameterclassname-method-sqlserverparametermetadata"></a>getParameterClassName 方法 (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索指定 Java 类的完全限定名称，而该 Java 类的实例应传递给 [SQLServerPreparedStatement](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) 类中的 [setObject](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getParameterClassName(int param)  
```  
  
#### <a name="parameters"></a>parameters  
 *param*  
  
 指示参数索引的 int  。  
  
## <a name="return-value"></a>返回值  
 包含完全限定类名称的 String  。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getParameterClassName 方法是由 java.sql.ParameterMetaData 接口中的 getParameterClassName 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerParameterMetaData 方法](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 成员](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 类](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
