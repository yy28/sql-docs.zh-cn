---
title: getSchemaTerm 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSchemaTerm
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3e4a400f-0859-4ac3-983e-c25633b33683
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b89f687575cfb2beb3a688587ea173788855fb09
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622396"
---
# <a name="getschematerm-method-sqlserverdatabasemetadata"></a>getSchemaTerm 方法 (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  检索与此数据库中的“架构”对应的首选术语。  
  
## <a name="syntax"></a>语法  
  
```  
  
public java.lang.String getSchemaTerm()  
```  
  
## <a name="return-value"></a>返回值  
 一个包含首选术语的字符串。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getSchemaTerm 方法由 java.sql.DatabaseMetaData 接口中的 getSchemaTerm 方法指定。  
  
 将 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 用于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库时，此方法将返回“架构”作为首选术语。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerDatabaseMetaData 方法](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 成员](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 类](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
