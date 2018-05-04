---
title: 国家/地区字符集支持 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4fceacfd-df4f-40cd-b7a2-5e5e58a5979f
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a0dcdb844c017a708d607570263717f2eaa56a39
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="national-character-set-support"></a>区域字符集支持
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  JDBC 驱动程序提供对 JDBC 4.0 API 的支持，后者包括新的区域字符集转换 API 方法。 这种支持包括新 setter、 getter 和更新程序方法**NCHAR**， **NVARCHAR**， **LONGNVARCHAR**，和**NCLOB** JDBC 类型。  
  
 下面是支持区域字符集转换的新增 getter、setter 和 updater 方法的列表：  
  
-   [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md): [setNString](../../connect/jdbc/reference/setnstring-method-int-java-lang-string.md)， [setNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)， [setNClob](../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md)。  
  
-   [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md): [getNClob](../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)， [getNString](../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md)， [getNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)， [setNString](../../connect/jdbc/reference/setnstring-method-sqlservercallablestatement.md)， [setNCharacterStream](../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)， [setNClob](../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)。  
  
-   [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md): [getNClob](../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md)， [getNString](../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)， [getNCharacterStream](../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)， [updateNClob](../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)， [updateNString](../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md)， [updateNCharacterStream](../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)。  
  
> [!NOTE]  
>  要在应用程序中使用这些方法，必须将 classpath 设置为包含 sqljdbc4.jar 文件。  
  
 若要发送到服务器以 Unicode 格式的字符串参数，应用程序应使用新的 JDBC 4.0 国家字符集方法;设置或**sendStringParametersAsUnicode**连接属性设置为"**true**"时使用的非 national 字符方法。 建议尽可能使用新的 JDBC 4.0 区域字符方法。 有关详细信息**sendStringParametersAsUnicode**连接属性，请参阅[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
## <a name="see-also"></a>另请参阅  
 [了解 JDBC 驱动程序数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
