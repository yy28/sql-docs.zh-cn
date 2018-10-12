---
title: isSigned 方法 (SQLServerParameterMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.isSigned
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1a4af386-e379-4a60-a107-a99e63a490ac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 718386cb23a0a53160d00351aff5175cea82c10d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47810125"
---
# <a name="issigned-method-sqlserverparametermetadata"></a>isSigned 方法 (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索指定参数的值能否为带正负号的数字。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean isSigned(int param)  
```  
  
#### <a name="parameters"></a>Parameters  
 *param*  
  
 指示参数索引的 int。  
  
## <a name="return-value"></a>返回值  
 如果指定参数可以包含带符号的数字，则为 true。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 isSigned 方法指定 java.sql.ParameterMetaData 接口中的 isSigned 方法。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerParameterMetaData 方法](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 成员](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 类](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
