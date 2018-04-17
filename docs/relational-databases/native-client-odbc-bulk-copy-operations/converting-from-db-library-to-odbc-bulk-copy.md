---
title: 从 DB 库转换为 ODBC 大容量复制 |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- converting DB-Library to ODBC bulk copy
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], DB-Library bulk copy
- ODBC, bulk copy operations
- DB-Library bulk copy
ms.assetid: 0bc15bdb-f19f-4537-ac6c-f249f42cf07f
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c5ef54d6c9d0eee2481941f8dc6c77fab737d3fc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="converting-from-db-library-to-odbc-bulk-copy"></a>从 DB-Library 转换到 ODBC 大容量复制
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  转换到 ODBC DB 库成批复制程序是简单，因为大容量复制函数支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序是类似于 Db-library 的大容量复制函数，但以下情况例外：  
  
-   DB-Library 应用程序将 DBPROCESS 结构的指针作为大容量复制函数的第一个参数进行传递。 在 ODBC 应用程序中，DBPROCESS 指针由 ODBC 连接句柄取代。  
  
-   Db-library 应用程序调用**BCP_SETL**之前连接到启用 DBPROCESS 上的大容量复制操作。 ODBC 应用程序改为调用[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)连接以启用连接句柄上的大容量操作之前：  
  
    ```  
    SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP,  
        (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
    ```  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序不支持 DB 库消息和错误处理程序; 你必须调用**SQLGetDiagRec**以获取错误和消息由 ODBC 大容量复制函数引发。 大容量复制函数的 ODBC 版本返回标准的大容量复制返回代码 SUCCEED 或 FAILED，而不是 ODBC 样式的返回代码，比如 SQL_SUCCESS 或 SQL_ERROR。  
  
-   指定 Db-library 值[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)*varlen*参数解释不同于 ODBC **bcp_bind * * * cbData*参数。  
  
    |指示条件|Db-library *varlen*值|ODBC *cbData*值|  
    |-------------------------|--------------------------------|-------------------------|  
    |提供 Null 值|0|-1 (SQL_NULL_DATA)|  
    |提供变量数据|-1|-10 (SQL_VARLEN_DATA)|  
    |零长度字符或二进制字符串|不适用|0|  
  
     在 Db-library， *varlen*值-1 指示，正在提供可变长度数据，这会在 ODBC *cbData*被解释为表示只有 NULL 值正在提供。 更改任何 Db-library *varlen* -1 到 SQL_VARLEN_DATA 及任何规范*varlen* 0 到 SQL_NULL_DATA 的规范。  
  
-   Db-library  **bcp_colfmt * * * file_collen*和 ODBC [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)*cbUserData * 具有同样的问题作为 **bcp_bind * * * varlen*和*cbData*参数如上所示。 更改任何 Db-library *file_collen* -1 到 SQL_VARLEN_DATA 及任何规范*file_collen* 0 到 SQL_NULL_DATA 的规范。  
  
-   *IValue* ODBC 参数[bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)函数是 void 指针。 在 DB 库， *iValue*为整数。 将值转换为 ODBC *iValue*为 void *。  
  
-   **Bcp_control**选项 BCPMAXERRS 指定大容量复制操作失败之前，单独的行数可以具有错误。 默认值为 BCPMAXERRS DB 库版本中为 0 （在第一个错误失败） **bcp_control**和 ODBC 版本中的 10。 必须更改 Db-library 应用程序依赖于默认值 0 终止批量复制操作以调用 ODBC **bcp_control**将 BCPMAXERRS 设为 0。  
  
-   ODBC **bcp_control**函数支持以下选项的 DB 库版本不支持**bcp_control**:  
  
    -   BCPODBC  
  
         当设置为 TRUE 时，指定**datetime**和**smalldatetime**值保存在字符格式将具有 ODBC 时间戳转义序列前缀和后缀。 这仅适用于 BCP_OUT 操作。  
  
         与设置为 FALSE，BCPODBC **datetime**值转换为字符字符串输出为：  
  
        ```  
        1997-01-01 00:00:00.000  
        ```  
  
         与设置为 TRUE，相同的 BCPODBC **datetime**值输出为：  
  
        ```  
        {ts '1997-01-01 00:00:00.000' }  
        ```  
  
    -   BCPKEEPIDENTITY  
  
         设置为 TRUE 时，指定大容量复制函数插入为具有标识约束的列提供的数据值。 如果未进行设置，则为插入的行生成新标识值。  
  
    -   BCPHINTS  
  
         指定各种大容量复制优化措施。 该选项无法在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 6.5 或更早版本上使用。  
  
    -   BCPFILECP  
  
         指定大容量复制文件的代码页。  
  
    -   BCPUNICODEFILE  
  
         指定字符模式大容量复制文件是 Unicode 文件。  
  
-   ODBC **bcp_colfmt**函数不支持*file_type* SQLCHAR 指示器因为它与 ODBC SQLCHAR typedef 冲突。 改用 SQLCHARACTER **bcp_colfmt**。  
  
-   大容量复制函数，使用的格式的 ODBC 版本**datetime**和**smalldatetime**字符字符串中的值是 yyyy-月-日 hh:mm:ss.sss; 的 ODBC 格式**smalldatetime**值使用 yyyy mm dd hh: mm: ODBC 格式。  
  
     大容量复制函数的 DB 库版本接受**datetime**和**smalldatetime**使用几种格式的字符字符串中的值：  
  
    -   默认格式是*mmm dd yyyy hh:mmxx*其中*xx*是 AM 或 PM。  
  
    -   **datetime**和**smalldatetime**字符 DB Library 所支持的任何格式的字符串**dbconvert**函数。  
  
    -   当**使用国际设置**上 Db-library 框被选中**选项**选项卡[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端网络实用工具 Db-library 大容量复制函数还接受区域中的日期为客户端计算机注册表的区域设置定义的日期格式。  
  
     Db-library 大容量复制函数不接受 ODBC **datetime**和**smalldatetime**格式。  
  
     如果 SQL_SOPT_SS_REGIONALIZE 语句属性设置为 SQL_RE_ON，则 ODBC 大容量复制函数接受的日期格式可以是为客户端计算机注册表的区域设置定义的区域日期格式。  
  
-   在输出时才**money**中字符的格式、 ODBC 大容量复制函数提供四位数的精度和没有逗号分隔符，则为值DB 库版本仅提供两个位精度，并包括逗号分隔符。  
  
## <a name="see-also"></a>另请参阅  
 [执行大容量复制操作&#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)   
 [大容量复制函数](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
