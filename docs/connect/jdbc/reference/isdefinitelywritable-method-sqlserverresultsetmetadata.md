---
title: isDefinitelyWritable 方法 (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.isDefinitelyWritable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7650e89a-dc8e-43ca-8eb2-f962f1a4b4ae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 49ca65fc7fd2c7768db81460e331d960bad1c5ea
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67977646"
---
# <a name="isdefinitelywritable-method-sqlserverresultsetmetadata"></a>isDefinitelyWritable 方法 (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指示指定列上的写入操作是否将一定成功。  
  
## <a name="syntax"></a>语法  
  
```  
  
public boolean isDefinitelyWritable(int column)  
```  
  
#### <a name="parameters"></a>parameters  
 *column*  
  
 指示列索引的 int  。  
  
## <a name="return-value"></a>返回值  
 如果列写入操作将一定成功，则为“true”  。 否则为 **false**。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>备注  
 此 isDefinitelyWritable 方法是由 java.sql.ResultSetMetaData 接口中的 isDefinitelyWritable 方法指定的。  
  
> [!NOTE]  
>  将 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库一起使用时，此方法会始终返回 false。  
  
## <a name="see-also"></a>另请参阅  
 [SQLServerResultSetMetaData 方法](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 成员](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 类](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
