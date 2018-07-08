---
title: 从 Db-library 转换到 ODBC 大容量复制 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
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
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 853e10c8db0baba2093266cd4aa12d3370136b1f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37417466"
---
# <a name="converting-from-db-library-to-odbc-bulk-copy"></a>从 DB-Library 转换到 ODBC 大容量复制
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  将 Db-library 大容量复制程序转换到 ODBC 很容易，因为大容量复制函数支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序将类似于 Db-library 大容量复制函数，但存在以下例外：  
  
-   DB-Library 应用程序将 DBPROCESS 结构的指针作为大容量复制函数的第一个参数进行传递。 在 ODBC 应用程序中，DBPROCESS 指针由 ODBC 连接句柄取代。  
  
-   Db-library 应用程序调用**BCP_SETL**连接以便在 DBPROCESS 上的大容量复制操作之前。 ODBC 应用程序改为调用[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)连接以便启用连接句柄上的大容量操作之前：  
  
    ```  
    SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP,  
        (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
    ```  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序不支持 Db-library 消息和错误处理程序; 必须调用**SQLGetDiagRec**获取错误和消息由 ODBC 大容量复制函数引发。 大容量复制函数的 ODBC 版本返回标准的大容量复制返回代码 SUCCEED 或 FAILED，而不是 ODBC 样式的返回代码，比如 SQL_SUCCESS 或 SQL_ERROR。  
  
-   DB 库指定的值[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)*varlen*参数以不同方式解释与 ODBC **bcp_bind * * * cbData*参数。  
  
    |指示条件|Db-library *varlen*值|ODBC *cbData*值|  
    |-------------------------|--------------------------------|-------------------------|  
    |提供 Null 值|0|-1 (SQL_NULL_DATA)|  
    |提供变量数据|-1|-10 (SQL_VARLEN_DATA)|  
    |零长度字符或二进制字符串|不适用|0|  
  
     在 Db-library *varlen*值为-1 指示，正在提供可变长度数据，在 ODBC *cbData*转译为表示为正在提供仅 NULL 值。 更改任何 Db-library *varlen*规范为 sql_varlen_data，则为-1 并将任何*varlen*规范 0 为 SQL_NULL_DATA。  
  
-   Db-library  **bcp_colfmt * * * file_collen*和 ODBC [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)* cbUserData * 具有同样的问题作为 **bcp_bind * * * varlen*并*cbData*上面记下的参数。 更改任何 Db-library *file_collen*规范为 sql_varlen_data，则为-1 并将任何*file_collen*规范 0 为 SQL_NULL_DATA。  
  
-   *IValue*参数的 ODBC [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)函数是 void 指针的指针。 在 Db-library *iValue*是整数。 将值转换为 ODBC *iValue*为 void *。  
  
-   **Bcp_control**选项 BCPMAXERRS 指定在多少单独行大容量复制操作失败前可以有错误。 BCPMAXERRS 的默认值为 0 （在第一个错误的故障） 中的 Db-library 版本**bcp_control**和 10 中的 ODBC 版本。 依赖于默认值为 0 以终止大容量复制操作的 Db-library 应用程序必须更改为调用 ODBC **bcp_control**将 BCPMAXERRS 设置为 0。  
  
-   ODBC **bcp_control**函数支持以下选项不支持的 Db-library 版本**bcp_control**:  
  
    -   BCPODBC  
  
         当设置为 TRUE，则指定的**datetime**并**smalldatetime**以字符格式保存的值将有 ODBC 时间戳转义序列前缀和后缀。 这仅适用于 BCP_OUT 操作。  
  
         设置为 FALSE，bcpodbc **datetime**值转换为字符字符串输出为：  
  
        ```  
        1997-01-01 00:00:00.000  
        ```  
  
         Bcpodbc 设置为 TRUE，则相同**datetime**值输出为：  
  
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
  
-   ODBC **bcp_colfmt**函数不支持*file_type* SQLCHAR 指示器因为它与 ODBC SQLCHAR typedef 冲突。 有关使用 SQLCHARACTER **bcp_colfmt**。  
  
-   在大容量复制函数，用于处理格式的 ODBC 版本**datetime**并**smalldatetime**字符字符串中的值是年-月-日 hh:mm:ss.sss; ODBC 格式**smalldatetime**值使用 ODBC 格式： 年-月-日分： 秒。  
  
     大容量复制函数的 Db-library 版本接受**datetime**并**smalldatetime**中使用多种格式的字符串值：  
  
    -   默认格式是*mmm dd yyyy hh: mmxx*其中*xx*是 AM 或 PM。  
  
    -   **日期时间**并**smalldatetime** DB Library 所支持的任何格式的字符串**dbconvert**函数。  
  
    -   当**使用国际设置**DB 库已选中复选框**选项**选项卡[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端网络实用工具的 Db-library 大容量复制函数可接受的日期位于区域定义客户端计算机注册表的区域设置日期格式。  
  
     Db-library 大容量复制函数不接受 ODBC **datetime**并**smalldatetime**格式。  
  
     如果 SQL_SOPT_SS_REGIONALIZE 语句属性设置为 SQL_RE_ON，则 ODBC 大容量复制函数接受的日期格式可以是为客户端计算机注册表的区域设置定义的区域日期格式。  
  
-   在输出时才**资金**字符格式、 ODBC 大容量复制函数提供四位数精度和没有逗号分隔符; 中的值Db-library 版本仅提供两位数精度，并且包含逗号分隔符。  
  
## <a name="see-also"></a>请参阅  
 [执行大容量复制操作&#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)   
 [大容量复制函数](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
