---
title: getScale 方法 (SQLServerParameterMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.getScale
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7b8d8d9c-74aa-4e6e-88f1-2fc5c74004ae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4e55fe6d5407cb9ab46f57e125f34d4e14dcdb9d
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921760"
---
# <a name="getscale-method-sqlserverparametermetadata"></a>getScale 方法 (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索指定参数的小数点右侧的位数。  
  
## <a name="syntax"></a>语法  
  
```  
  
public int getScale(int param)  
```  
  
#### <a name="parameters"></a>parameters  
 *param*  
  
 指示参数索引的 int  。  
  
## <a name="return-value"></a>返回值  
 指示指定参数的确定位数的 int  。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 getScale 方法是由 java.sql.ParameterMetaData 接口中的 getScale 方法指定的。  
  
 此方法获取小数点右侧的列位数。 对于不具有小数点的类型，此方法返回“0”。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerParameterMetaData 方法](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 成员](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 类](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
