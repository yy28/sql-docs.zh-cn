---
title: SQLConnect 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConnect
helpviewer_keywords:
- SQLConnect function [ODBC]
ms.assetid: 59075e46-a0ca-47bf-972a-367b08bb518d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 530a5acf9cc7c0de375906279aff2bc6a05ec8a0
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53213691"
---
# <a name="sqlconnect-function"></a>SQLConnect 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：ISO 92  
  
 **摘要**  
 **SQLConnect**建立到驱动程序和数据源的连接。 连接句柄所引用有关连接到数据源，包括状态、 事务状态和错误信息的所有信息的存储。  
  
## <a name="syntax"></a>语法  
  
```  
  
SQLRETURN SQLConnect(  
     SQLHDBC        ConnectionHandle,  
     SQLCHAR *      ServerName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      UserName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      Authentication,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>参数  
 *ConnectionHandle*  
 [输入]连接句柄。  
  
 *ServerName*  
 [输入]数据源名称。 数据可能不位于该程序，在同一台计算机上，也可以在网络上的某个位置的另一台计算机上。 有关应用程序如何选择数据源的信息，请参阅[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 *NameLength1*  
 [输入]长度 **ServerName*以字符为单位。  
  
 *UserName*  
 [输入]用户标识符。  
  
 *NameLength2*  
 [输入]长度 **用户名*以字符为单位。  
  
 *身份验证*  
 [输入]身份验证的字符串 （通常是密码）。  
  
 *NameLength3*  
 [输入]长度 **身份验证*以字符为单位。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLConnect**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用来获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_DBC 和一个*处理*的*ConnectionHandle*。 下表列出了通常由返回的 SQLSTATE 值**SQLConnect** ，并解释了此函数; 每个上下文中的表示法"（数据挖掘）"之前 SQLSTATEs 返回由驱动程序管理器的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另有说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S02|选项值已更改|该驱动程序不支持的指定的值*ValuePtr*中的参数**SQLSetConnectAttr**和替换一个相近的值。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08001|客户端无法建立连接|该驱动程序无法建立与数据源的连接。|  
|08002|在使用的连接名称|(DM) 指定*ConnectionHandle*已用于建立连接并与数据源和连接时仍处于打开或用户已浏览的连接。|  
|08004|服务器拒绝连接|数据源实现定义的原因拒绝建立连接。|  
|08S01|通讯链接失败|该驱动程序和驱动程序已尝试连接到数据源之间的通信链接失败之前函数已完成处理。|  
|28000|无效的授权说明|为参数指定的值*用户名*或为参数指定的值*身份验证*违反定义的数据源的限制。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义任何特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中 *\*MessageText*缓冲区描述错误以及其原因。|  
|HY001|内存分配错误|(DM) 的驱动程序管理器无法分配支持执行或完成该函数所需的内存。|  
|HY008|操作已取消|异步处理的已启用*ConnectionHandle*。 **SQLConnect**调用函数，和之前执行完毕[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)上调用了*ConnectionHandle*，然后**SQLConnect**上再次调用函数*ConnectionHandle*。<br /><br /> 或者， **SQLConnect**调用函数，和之前执行完毕**SQLCancelHandle**上调用了*ConnectionHandle*来自不同线程中多线程应用程序。|  
|HY010|函数序列错误|(DM) 的调用以异步方式执行的函数 （不是此类似） *ConnectionHandle*和仍在执行时调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 为参数指定的值*NameLength1*， *NameLength2*，或*NameLength3*小于 0，但不是等于 SQL_NTS。<br /><br /> (DM) 为参数指定的值*NameLength1*超出数据源名称的最大长度。|  
|HYT00|超时时间已到|查询超时期限过期之前完成的数据源的连接。 通过设置超时期限**SQLSetConnectAttr**，SQL_ATTR_LOGIN_TIMEOUT。|  
|HY114|驱动程序不支持连接级别的异步函数执行|(DM) 应用程序启用对连接句柄之前建立的连接的异步操作。 但是，该驱动程序不支持连接句柄上的异步操作。|  
|HYT01|连接超时时间已到|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 指定数据源名称的驱动程序不支持该函数。|  
|IM002|找不到数据源和未指定的默认驱动程序|(DM) 的数据源名称参数中指定*ServerName*系统信息中未找到，也没有默认驱动程序规范。|  
|IM003|指定的驱动程序不会连接到|(DM) 数据中列出的驱动程序源规范系统信息中的找不到或可能不会连接到某些其他原因。|  
|IM004|SQL_HANDLE_ENV 上的驱动程序的 SQLAllocHandle 失败|(DM) 期间**SQLConnect**，驱动程序管理器调用的驱动程序**SQLAllocHandle**函数与*HandleType* SQL_HANDLE_ENV 和驱动程序返回了一个错误。|  
|IM005|SQL_HANDLE_DBC 上的驱动程序的 SQLAllocHandle 失败|(DM) 期间**SQLConnect**，驱动程序管理器调用的驱动程序**SQLAllocHandle**函数与*HandleType* SQL_HANDLE_DBC 和驱动程序返回了一个错误。|  
|IM006|驱动程序的 SQLSetConnectAttr 失败|期间**SQLConnect**，驱动程序管理器调用的驱动程序**SQLSetConnectAttr**函数和驱动程序返回了错误。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|IM009|无法连接到转换 DLL|该驱动程序无法连接到转换为数据源指定的 DLL。|  
|IM010|数据源名称太长|（数据挖掘）  *\*ServerName*已超过 SQL_MAX_DSN_LENGTH 个字符。|  
|IM014|指定的 DSN 包含驱动程序和应用程序体系结构不匹配|(DM) 32 位应用程序使用 DSN 连接到 64 位驱动程序;反之亦然。|  
|IM015|驱动程序的 SQLConnect SQL_HANDLE_DBC_INFO_HANDLE 上失败|如果驱动程序将返回 SQL_ERROR，驱动程序管理器将向应用程序返回 SQL_ERROR，并且连接将失败。<br /><br /> 有关 SQL_HANDLE_DBC_INFO_TOKEN 详细信息，请参阅[ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。|  
|IM017|轮询异步通知模式中禁用|只要使用通知模型，将禁用轮询。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上以前的异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用通知模式，则**SQLCompleteAsync**必须要对其进行后期处理并完成该操作的句柄上调用。|  
|S1118|驱动程序不支持异步通知|当驱动程序不支持异步通知时，您不能设置 SQL_ATTR_ASYNC_DBC_EVENT 或 SQL_ATTR_ASYNC_DBC_RETCODE_PTR。|  
  
## <a name="comments"></a>注释  
 应用程序使用的原因的信息**SQLConnect**，请参阅[使用 SQLConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)。  
  
 驱动程序管理器在应用程序调用函数之前不会连接到驱动程序 (**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**) 连接到驱动程序。 在此之前，驱动程序管理器具有其自己的句柄的工作和管理连接信息。 当应用程序调用连接函数时，驱动程序管理器将检查驱动程序当前是否连接到指定*ConnectionHandle*:  
  
-   如果驱动程序未连接到，驱动程序管理器连接到该驱动程序并调用**SQLAllocHandle**与*HandleType*设为 SQL_HANDLE_ENV， **SQLAllocHandle**与*HandleType*设为 SQL_HANDLE_DBC， **SQLSetConnectAttr** （如果应用程序指定任何连接属性），并在驱动程序中的连接函数。 驱动程序管理器返回 SQLSTATE IM006 (驱动程序的**SQLSetConnectOption**失败) 和连接函数如果驱动程序返回的错误 SQL_SUCCESS_WITH_INFO **SQLSetConnectAttr**。 有关详细信息，请参阅[连接到数据源或驱动程序](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)。  
  
-   如果指定的驱动程序已连接到在*ConnectionHandle*，驱动程序管理器驱动程序中调用仅连接函数。 在这种情况下，该驱动程序必须确保所有连接都属性*ConnectionHandle*维护其当前设置。  
  
-   如果不同的驱动程序连接到，驱动程序管理器会调用**SQLFreeHandle**与*HandleType*设为 SQL_HANDLE_DBC，然后，如果没有其他驱动程序连接到该环境中，将调用**SQLFreeHandle**与*HandleType*设为 SQL_HANDLE_ENV 连接驱动程序中，然后断开连接该驱动程序。 然后，它执行与驱动程序时未连接到相同的操作。  
  
 然后，该驱动程序分配句柄并初始化自身。  
  
 当应用程序调用**SQLDisconnect**，驱动程序管理器调用**SQLDisconnect**驱动程序中。 但是，它不会断开该驱动程序。 这在反复连接到和从数据源断开连接的应用程序的内存中保留该驱动程序。 当应用程序调用**SQLFreeHandle**与*HandleType*设为 SQL_HANDLE_DBC，驱动程序管理器调用**SQLFreeHandle**与*HandleType*设为 SQL_HANDLE_DBC，然后**SQLFreeHandle**与*HandleType*设为 SQL_HANDLE_ENV 在驱动程序，然后断开连接，驱动程序。  
  
 ODBC 应用程序可以建立多个连接。  
  
## <a name="driver-manager-guidelines"></a>驱动程序管理器指导原则  
 内容 **ServerName*影响驱动程序管理器和一个驱动程序如何协同工作以建立与数据源的连接。  
  
-   如果\* *ServerName*包含有效数据源名称，驱动程序管理器的系统信息中查找相应的数据源规范并将连接到关联的驱动程序。 驱动程序管理器将每个传递**SQLConnect**向驱动程序的参数。  
  
-   如果找不到数据源名称或*ServerName*是 null 指针，驱动程序管理器查找默认数据源说明，并连接到关联的驱动程序。 驱动程序管理器将传递给驱动程序*用户名*并*身份验证*以未经修改的参数和"DEFAULT"用于*ServerName*参数。  
  
-   如果*ServerName*参数为"DEFAULT"，驱动程序管理器查找默认数据源说明，并连接到关联的驱动程序。 驱动程序管理器将每个传递**SQLConnect**向驱动程序的参数。  
  
-   如果找不到数据源名称或*ServerName*为 null 指针，并且默认值的数据源规范不存在，则驱动程序管理器返回具有 SQLSTATE IM002 SQL_ERROR （数据源找不到名称和无默认值指定驱动程序）。  
  
 它已连接到由驱动程序管理器后，驱动程序可以在系统信息中查找其相应的数据源规范和使用规范中的特定于驱动程序的信息来完成其组的所需的连接信息。  
  
 如果数据源的系统信息中指定默认转换库，则该驱动程序连接到它。 可以通过调用连接到不同的转换库**SQLSetConnectAttr**使用 SQL_ATTR_TRANSLATE_LIB 属性。 可以通过调用指定转换选项**SQLSetConnectAttr** SQL_ATTR_TRANSLATE_OPTION 属性。  
  
 如果驱动程序支持**SQLConnect**，该驱动程序的系统信息的驱动程序关键字部分必须包含**ConnectFunctions**的第一个字符的关键字设置为"Y"。  
  
### <a name="connection-pooling"></a>连接池  
 连接池允许应用程序以重复使用已创建的连接。 当启用连接池并**SQLConnect**调用时，驱动程序管理器尝试建立连接使用的是已被指定为连接池的环境中的连接池的一部分的连接。 此环境是在池中使用的连接的所有应用程序使用一个共享的环境。  
  
 在环境分配通过调用之前启用连接池**SQLSetEnvAttr**将 SQL_ATTR_CONNECTION_POOLING 设置为 SQL_CP_ONE_PER_DRIVER （它指定每个驱动程序的一个池的最大值） 或 SQL_CP_ONE_PER_HENV（指定每个环境的一个池的最大值）。 **SQLSetEnvAttr**这种情况下使用调用*EnvironmentHandle*设置为 null，这使得进程级别属性的属性。 如果 SQL_ATTR_CONNECTION_POOLING 设置为 SQL_CP_OFF，已禁用连接池。  
  
 已启用连接池后， **SQLAllocHandle**与*HandleType*设为 SQL_HANDLE_ENV 调用分配一个环境。 此调用分配的环境是一个共享的环境，因为已启用连接池。 但是，只有不确定将使用的环境**SQLAllocHandle**与*HandleType*设为 SQL_HANDLE_DBC 调用。  
  
 **SQLAllocHandle**与*HandleType*设为 SQL_HANDLE_DBC 调用来分配连接。 驱动程序管理器尝试查找匹配应用程序设置的环境属性的现有共享的环境。 如果不存在任何此类环境，将创建一个作为一种隐式*共享的环境*。 如果找到匹配的共享的环境，环境句柄返回给应用程序和其引用计数会递增。  
  
 但是，只有不确定将使用的连接**SQLConnect**调用。 此时，驱动程序管理器尝试在应用程序请求的条件相匹配的连接池中查找现有连接。 这些条件包括对的调用中所请求的连接选项**SQLConnect** (的值*ServerName*，*用户名*，和*身份验证*关键字) 和任何连接的属性集，因为**SQLAllocHandle**与*HandleType*设为 SQL_HANDLE_DBC 调用。 驱动程序管理器检查的相应连接关键字和池中的连接中的属性对这些条件。 如果找到匹配项，则使用池中的连接。 如果不找到任何匹配项，则创建新的连接。  
  
 如果 SQL_ATTR_CP_MATCH 环境属性设置为 SQL_CP_STRICT_MATCH，匹配必须为确切的池中使用的连接。 如果 SQL_ATTR_CP_MATCH 环境属性设置为 SQL_CP_RELAXED_MATCH，连接选项在调用**SQLConnect**必须匹配，而不是所有连接属性必须匹配。  
  
 将应用以下规则时的连接属性，所设置的应用程序，然后**SQLConnect**被调用时，与在池中的连接的连接属性不匹配：  
  
-   如果建立连接之前，必须设置连接属性：  
  
     如果 SQL_ATTR_CP_MATCH SQL_CP_STRICT_MATCH，SQL_ATTR_PACKET_SIZE 中已入池连接必须与应用程序设置的属性相同。 如果 SQL_CP_RELAXED_MATCH，SQL_ATTR_PACKET_SIZE 的值可能会不同。  
  
     SQL_ATTR_LOGIN_VALUE 的值不会影响匹配。  
  
-   如果之前或之后建立连接时，可以设置连接属性：  
  
     如果连接属性尚未设置应用程序，但尚未设置连接上的池中，并且没有默认值中已入池连接, 的连接属性重新设置为默认值，并声明一个匹配项。 如果没有默认值，已入池的连接不视为匹配项。  
  
     如果连接属性已由应用程序设置，但尚未设置连接上的池中，对该集由应用程序更改池的连接属性和声明匹配项。  
  
     如果连接属性已经设置了由应用程序，并且还已设置在连接上的池中，但这些值不匹配，则使用应用程序的连接属性的值，并声明匹配项。  
  
-   如果驱动程序特定的连接属性的值不完全相同且 SQL_ATTR_CP_MATCH 设置为 SQL_CP_STRICT_MATCH，不是使用池中的连接。  
  
 当应用程序调用**SQLDisconnect**断开连接，连接将返回到连接池，并且可供重复使用。  
  
### <a name="optimizing-connection-pooling-performance"></a>优化连接池性能  
 当涉及到分布式的事务时，就可以优化连接池使用的性能**SQL_DTC_TRANSITION_COST**，这是 SQLUINTEGER 位掩码。 引用转换的连接属性将从 0 的值不为零，SQL_ATTR_ENLIST_IN_DTC 的转换，反之亦然。 这是从连接未登记到分布式事务中登记在分布式事务中，反之亦然。 具体取决于如何驱动程序实现登记 （设置连接属性 SQL_ATTR_ENLIST_IN_DTC），这些转换可能会非常昂贵，因此应当避免为了获得最佳性能。  
  
 驱动程序返回的值包含以下位的任意组合：  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**，当设置，则意味着比从非零值转换到另一个非零值 （前面已登记的连接在其下一个事务中登记） 贵很多非零值转换为零。  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**，当设置，则意味着零转换为非零值是比使用其 SQL_ATTR_ENLIST_IN_DTC 属性已设置为零的连接贵很多。  
  
 没有与连接使用情况权衡性能。 如果驱动程序指示一个或多个这些过渡是昂贵，驱动程序管理器的连接池进程将保留在池中的更多连接，从而对此做出响应。 一些池中的连接是首选非事务性使用，而有些则首选事务使用。 但是，如果该驱动程序指出，这些转换并不昂贵，较少连接可用，可能交替使用非事务性和事务使用。  
  
 不支持 SQL_ATTR_ENLIST_IN_DTC 的驱动程序不需要支持 SQL_DTC_TRANSITION_COST。 支持 SQL_ATTR_ENLIST_IN_DTC，但不是 SQL_DTC_TRANSITION_COST 支持的驱动程序，请假定，转换并不昂贵，因为如果驱动程序返回此值为 0 （无设置位）。  
  
 尽管在 ODBC 3.5 中，ODBC 2 引入了 SQL_DTC_TRANSITION_COST。*x*驱动程序还可以支持它因为驱动程序管理器将查询此信息，不管驱动程序版本。  
  
### <a name="code-example"></a>代码示例  
 在以下示例中，应用程序分配环境和连接句柄。 然后，连接到具有用户 ID 约翰的销售订单数据源和密码 Sesame 并处理数据。 完成处理数据后，它与数据源断开连接并释放句柄。  
  
```  
// SQLConnect_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt;  
   SQLRETURN retcode;  
  
   SQLCHAR * OutConnStr = (SQLCHAR * )malloc(255);  
   SQLSMALLINT * OutConnStrLen = (SQLSMALLINT *)malloc(255);  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLCHAR*) "NorthWind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
### <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|分配句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|发现和枚举值来连接到数据源|[SQLBrowseConnect 函数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|与数据源断开连接|[SQLDisconnect 函数](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|连接到使用连接字符串或对话框中的数据源|[SQLDriverConnect 函数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|返回连接属性的设置|[SQLGetConnectAttr 函数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|将连接属性设置|[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
