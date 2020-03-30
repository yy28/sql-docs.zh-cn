---
title: getParameterType 方法 (SQLServerParameterMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.getParameterType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 638aca05-63e4-4d73-a9c8-e0442f775720
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bd9252827e7c7bec70636937bc89dd5390e68519
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67980957"
---
# <a name="getparametertype-method-sqlserverparametermetadata"></a>getParameterType 方法 (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索指定参数的 SQL 类型。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getParameterType(int param)  
```  
  
#### <a name="parameters"></a>parameters  
 *param*  
  
 指示参数索引的 int  。  
  
## <a name="return-value"></a>返回值  
 指示 java.sql.Types 中定义的 JDBC 类型代码的 int  。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getParameterType 方法是由 java.sql.ParameterMetaData 接口中的 getParameterType 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerParameterMetaData 方法](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 成员](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 类](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
