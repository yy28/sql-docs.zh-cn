---
title: getMoreResults 方法 (int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getMoreResults (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6419e5a8-8b3a-4d5b-8226-95865c52c723
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7d4fe32d7d1ac4be9a20923fc4d230ac64d1c8d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47667805"
---
# <a name="getmoreresults-method-int"></a>getMoreResults 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  移动到此 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 对象的下一个结果并根据给定模式所指定的说明处理任何当前打开的结果集对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
public final boolean getMoreResults(int mode)  
```  
  
#### <a name="parameters"></a>Parameters  
 模式  
  
 指示如何处理当前打开的结果集对象的 int。 必须是下列常量之一：  
  
 CLOSE_CURRENT_RESULT  
  
 KEEP_CURRENT_RESULT（JDBC 驱动程序不支持）  
  
 CLOSE_ALL_RESULTS  
  
## <a name="return-value"></a>返回值  
 如果返回的结果为一个结果集，则为 true。 否则为 **false**。  
  
## <a name="exceptions"></a>异常  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 此 getMoreResults 方法由 java.sql.Statement 接口中的 getMoreResults 方法指定。  
  
 如果在检索结果前调用 getMoreResults 方法，则该方法就会采用 mode 参数指定的行为方式并移动到下一个结果。  
  
> [!NOTE]  
>  JDBC 驱动程序不支持使用 KEEP_CURRENT_RESULT 常量。 如果使用该常量，将引发异常。  
  
## <a name="see-also"></a>另请参阅  
 [getMoreResults 方法 &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [SQLServerStatement 成员](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
