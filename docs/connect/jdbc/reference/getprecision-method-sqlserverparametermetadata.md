---
title: "getPrecision 方法 (SQLServerParameterMetaData) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerParameterMetaData.getPrecision
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8bd79484-bab6-423b-978f-d7ec7132ebeb
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8c80beecc510fb5f2d4190839e8bc4ca1c95602c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="getprecision-method-sqlserverparametermetadata"></a>getPrecision 方法 (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索十进制数字的指定参数的数目。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getPrecision(int param)  
```  
  
#### <a name="parameters"></a>Parameters  
 *param*  
  
 **Int** ，该值指示参数索引。  
  
## <a name="return-value"></a>返回值  
 **Int** ，该值指示指定的参数的精度。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.ParameterMetaData 接口中的 getPrecision 方法指定此 getPrecision 方法。  
  
 对于数字类型，此方法获取小数位数。 对于字符类型，此方法获取用字符表示的最大长度。 对于二进制类型，此方法获取用字节表示的最大长度。 如果位数未知，此方法将返回“0”。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerParameterMetaData 方法](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 成员](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 类](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  

