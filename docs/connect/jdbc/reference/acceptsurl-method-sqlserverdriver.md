---
title: acceptsURL 方法 (SQLServerDriver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDriver.acceptsURL
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fc744566-7191-4b15-9f76-b4b8087fb14a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68e12a39cb4a27f170b7f12705f17791bb40b649
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923707"
---
# <a name="acceptsurl-method-sqlserverdriver"></a>acceptsURL 方法 (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检查给定 URL 是否有效。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean acceptsURL(java.lang.String url)  
```  
  
#### <a name="parameters"></a>parameters  
 *url*  
  
 包含用于连接数据库的 URL 的 String  值。  
  
## <a name="return-value"></a>返回值  
 如果给定 URL 有效，则为 true  。 否则为 **false**。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 acceptsURL 方法是由 java.sql.Driver 接口中的 acceptsURL 方法指定的。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDriver 方法](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [SQLServerDriver 成员](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [SQLServerDriver 类](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
