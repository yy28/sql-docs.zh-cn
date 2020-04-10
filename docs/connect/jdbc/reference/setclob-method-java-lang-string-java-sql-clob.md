---
title: setClob 方法 (java.lang.String, java.sql.Clob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 256b5f55-7a6d-44fb-9a09-19fa39f19c35
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d4a3f54f499504cede4c3cca2d87c20c095eda23
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925302"
---
# <a name="setclob-method-javalangstring-javasqlclob"></a>setClob 方法 (java.lang.String, java.sql.Clob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将指定参数设置为指定的 Clob 对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final void setClob(java.lang.String parameterName,  
            java.sql.Clob x)  
```  
  
#### <a name="parameters"></a>parameters  
 parameterName   
  
 包含参数名称的字符串  。  
  
 *x*  
  
 Clob 对象。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 setClob 方法是由 java.sql.CallableStatement 接口中的 setClob 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [setClob 方法 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 成员](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
