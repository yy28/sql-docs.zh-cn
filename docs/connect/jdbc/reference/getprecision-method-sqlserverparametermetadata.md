---
title: getPrecision 方法 (SQLServerParameterMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.getPrecision
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8bd79484-bab6-423b-978f-d7ec7132ebeb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b0c6b7d8c69e1cc6bc4a9e8d239c3a47c24573d9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67980779"
---
# <a name="getprecision-method-sqlserverparametermetadata"></a>getPrecision 方法 (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索指定参数的小数位数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getPrecision(int param)  
```  
  
#### <a name="parameters"></a>Parameters  
 *param*  
  
 指示参数索引的 int  。  
  
## <a name="return-value"></a>返回值  
 指示指定参数精度的 int  。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getPrecision 方法由 getPrecision 方法在 Java.sql.parametermetadata 接口中指定。  
  
 对于数字类型，此方法获取小数位数。 对于字符类型，此方法获取用字符表示的最大长度。 对于二进制类型，此方法获取用字节表示的最大长度。 如果位数未知，此方法将返回“0”。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerParameterMetaData 方法](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 成员](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 类](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
