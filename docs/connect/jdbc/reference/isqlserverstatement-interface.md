---
title: ISQLServerStatement 接口 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7f83b514-6e76-4f37-baf3-a10db2010e7c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec01618ffa24c980733642ca66df5af0f234d172
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924739"
---
# <a name="isqlserverstatement-interface"></a>ISQLServerStatement 接口
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  表示 JDBC 语句功能的基本实现。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 中新增了此接口。  
  
 **包：** com.microsoft.sqlserver.jdbc  
  
 **扩展：** java.sql.Statement  
  
## <a name="syntax"></a>语法  
  
```  
  
public interface ISQLServerStatement  
```  
  
## <a name="remarks"></a>备注  
 此接口是由 [SQLServerStatement 类](../../../connect/jdbc/reference/sqlserverstatement-class.md)实现的。  
  
 此接口公开以下 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 特定的方法：  
  
|方法|有关详细信息，请参阅|  
|------------|-------------------------------|  
|public String getResponseBuffering|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|  
|public void setResponseBuffering|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序 API 参考](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
