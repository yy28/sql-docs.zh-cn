---
title: getSchemaTerm 方法 (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSchemaTerm
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3e4a400f-0859-4ac3-983e-c25633b33683
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dfa14c040aa8c399fa4993fe68347ffe61ee8f7b
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784704"
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
  
  
