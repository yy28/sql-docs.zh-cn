---
title: "getMoreResults 方法 (int) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerStatement.getMoreResults (int)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 6419e5a8-8b3a-4d5b-8226-95865c52c723
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 94667aabdcc08693f4f7a8647f9333a18053e956
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="getmoreresults-method-int"></a>getMoreResults 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  将移动到下一个结果此[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)对象并处理任何当前打开的结果集根据指定的给定模式的说明进行操作的对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final boolean getMoreResults(int mode)  
```  
  
#### <a name="parameters"></a>Parameters  
 *模式*  
  
 **Int** ，该值指示如何处理当前打开的结果集对象。 必须是以下常量之一：  
  
 CLOSE_CURRENT_RESULT  
  
 KEEP_CURRENT_RESULT（JDBC 驱动程序不支持）  
  
 CLOSE_ALL_RESULTS  
  
## <a name="return-value"></a>返回值  
 **true**如果返回的结果是一个结果集。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>注释  
 由 java.sql.Statement 接口中的 getMoreResults 方法指定此 getMoreResults 方法。  
  
 如果在检索结果之前调用 getMoreResults 方法，则其行为由指定*模式*自变量并且将移至下一个结果。  
  
> [!NOTE]  
>  JDBC 驱动程序不支持使用 KEEP_CURRENT_RESULT 常量。 如果使用该常量，将引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [getMoreResults 方法 &#40;SQLServerStatement &#41;](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
