---
title: setFloat 方法 (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setFloat
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 26d861da-bb6a-4197-8b32-13dc7781c2bb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ef88415db781721815be6de51c6b94303e59b07
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922297"
---
# <a name="setfloat-method-sqlservercallablestatement"></a>setFloat 方法 (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为给定的 float  值。  
  
## <a name="syntax"></a>语法  
  
```  
  
public void setFloat(java.lang.String sCol,  
                     float f)  
```  
  
#### <a name="parameters"></a>parameters  
 sCol   
  
 包含参数名称的字符串  。  
  
 *f*  
  
 float  值。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setFloat 方法是由 java.sql.CallableStatement 接口中的 setFloat 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 类](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
