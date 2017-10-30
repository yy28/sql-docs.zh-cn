---
title: "ISQLServerStatement 接口 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7f83b514-6e76-4f37-baf3-a10db2010e7c
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8865b6478b685231c4421166134fabde57aa70e7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="isqlserverstatement-interface"></a>ISQLServerStatement 接口
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示 JDBC 语句功能的基本实现。 此接口已添加到中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]JDBC Driver 3.0。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **扩展：** java.sql.Statement  
  
## <a name="syntax"></a>语法  
  
```  
  
public interface ISQLServerStatement  
```  
  
## <a name="remarks"></a>注释  
 此接口由实现[SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)。  
  
 此接口公开以下[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]的特定方法：  
  
|方法|有关详细信息，请参阅|  
|------------|-------------------------------|  
|public String getResponseBuffering|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|  
|public void setResponseBuffering|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  

