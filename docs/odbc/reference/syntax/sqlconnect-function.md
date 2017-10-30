---
title: "SQLConnect 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f3954538b63739fe19435aeb5cd30449edbc9d24
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlconnect-function"></a>SQLConnect 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLConnect**建立到驱动程序和数据源的连接。 连接句柄引用的数据源，包括状态、 事务状态和错误信息与连接有关的所有信息的存储。  
  
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
 [输入]数据源名称。 数据可能位于与该程序，在同一计算机上，也可以在网络上的某个位置的另一台计算机上。 有关如何应用程序选择数据源的信息，请参阅[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 *NameLength1*  
 [输入]长度 **ServerName*以字符为单位。  
  
 *UserName*  
 [输入]用户标识符。  
  
 *NameLength2*  
 [输入]长度 **用户名*以字符为单位。  
  
 *身份验证*  
 [输入]身份验证字符串 （通常为密码）。  
  
 *NameLength3*  
 [输入]长度 **身份验证*以字符为单位。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLConnect**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，关联的 SQLSTATE 值可以通过调用获取**SQLGetDiagRec**与*HandleType*的 SQL_HANDLE_DBC 和*处理*的*ConnectionHandle*。 下表列出了通常返回的 SQLSTATE 值**SQLConnect**并说明的上下文中的此函数; 每个表示法"(DM)"之前 SQLSTATEs 返回由驱动程序管理器中的说明。 与每个 SQLSTATE 值关联的返回代码是 SQL_ERROR，除非另外说明。  
  
|SQLSTATE|错误|Description|  
|--------------|-----------|-----------------|  
|01000|常规警告|特定于驱动程序的信息性消息。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|01S02 的警告|选项值已更改|该驱动程序不支持的指定的值*ValuePtr*中的参数**SQLSetConnectAttr**和替换类似的值。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|08001|客户端无法建立连接|该驱动程序无法建立与数据源的连接。|  
|08002|连接名称已在使用|(DM) 指定*ConnectionHandle*已用于建立与数据源的连接和连接时仍处于打开状态，或者用户浏览它的连接。|  
|08004|服务器拒绝连接|数据源实现定义的原因拒绝建立连接。|  
|08S01|通讯链接失败|在函数完成处理之前失败的驱动程序和驱动程序已尝试连接到数据源之间的通信链接。|  
|28000|无效的授权说明|为参数指定的值*用户名*或指定自变量的值*身份验证*违反数据源定义的限制。|  
|HY000|常规错误|有关其中没有任何特定的 SQLSTATE 和为其定义没有特定于实现的 SQLSTATE 出错。 返回的错误消息**SQLGetDiagRec**中* \*MessageText*缓冲区描述错误以及其可能的原因。|  
|HY001|内存分配错误|(DM) 驱动程序管理器无法分配支持执行或函数完成所需的内存。|  
|HY008|已取消操作|为启用了异步处理*ConnectionHandle*。 **SQLConnect**调用函数，并且它之前完成执行， [SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)上调用了*ConnectionHandle*，然后**SQLConnect**函数上调用了再次*ConnectionHandle*。<br /><br /> 或者， **SQLConnect**调用函数，并且它之前完成执行， **SQLCancelHandle**上调用了*ConnectionHandle*来自中的不同线程多线程应用程序。|  
|HY010|函数序列错误|(DM) 以异步方式执行的函数 （而不是此的一个） 曾为*ConnectionHandle*和仍在执行时调用此函数。|  
|HY013|内存管理错误|无法处理函数调用，因为基础内存对象无法访问，可能是由于内存不足的情况。|  
|HY090|字符串或缓冲区长度无效|(DM) 参数指定的值*NameLength1*， *NameLength2*，或*NameLength3*小于 0，但与 sql_nts 以不相等。<br /><br /> (DM) 参数指定的值*NameLength1*超过数据源名称的最大长度。|  
|HYT00|超时时间已到|查询超时期限过期之前完成数据源的连接。 通过设置的超时期限**SQLSetConnectAttr**，SQL_ATTR_LOGIN_TIMEOUT。|  
|HY114|驱动程序不支持连接级别的异步函数执行|(DM) 启用应用程序上连接句柄之前建立的连接的异步操作。 但是，该驱动程序不支持连接句柄上的异步操作。|  
|HYT01|连接超时过期|连接超时期限过期之前的数据源响应此请求。 通过设置连接超时期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驱动程序不支持此函数|(DM) 的数据源名称指定的驱动程序不支持该函数。|  
|IM002|找不到的数据源和未指定的默认驱动程序|(DM) 的数据源名称参数中指定*ServerName*中系统信息中，未找到，也没有默认驱动程序规范。|  
|IM003|指定的驱动程序不会连接到|(DM) 数据中列出的驱动程序中的系统信息的源规范找不到或无法未连接到其他原因。|  
|IM004|驱动程序的 SQLAllocHandle SQL_HANDLE_ENV 上失败|(DM) 期间**SQLConnect**，驱动程序管理器调用驱动程序的**SQLAllocHandle**起作用*HandleType*的 SQL_HANDLE_ENV 和驱动程序返回了一个错误。|  
|IM005|驱动程序的 SQLAllocHandle SQL_HANDLE_DBC 上失败|(DM) 期间**SQLConnect**，驱动程序管理器调用驱动程序的**SQLAllocHandle**起作用*HandleType*的 SQL_HANDLE_DBC 和驱动程序返回了一个错误。|  
|IM006|驱动程序的 SQLSetConnectAttr 失败|期间**SQLConnect**，驱动程序管理器调用驱动程序的**SQLSetConnectAttr**函数和驱动程序返回了一个错误。 （函数返回 SQL_SUCCESS_WITH_INFO。）|  
|IM009|无法连接到转换 DLL|该驱动程序无法连接到转换为数据源指定的 DLL。|  
|IM010|数据源名称太长|(DM) * \*ServerName*已超过 SQL_MAX_DSN_LENGTH 个字符。|  
|IM014|指定的 DSN 包含的驱动程序和应用程序体系结构不匹配|(DM) 32 位应用程序使用连接到 64 位驱动程序; DSN反之亦然。|  
|IM015|驱动程序的 SQLConnect SQL_HANDLE_DBC_INFO_HANDLE 上失败|如果驱动程序返回 SQL_ERROR，驱动程序管理器将返回 SQL_ERROR 到应用程序，则连接将失败。<br /><br /> 有关 SQL_HANDLE_DBC_INFO_TOKEN 的详细信息，请参阅[开发中使用 ODBC 驱动程序的连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。|  
|IM017|在异步通知模式中禁用轮询|使用通知模型，则每当轮询处于禁用状态。|  
|IM018|**SQLCompleteAsync**尚未调用以完成此句柄上的上一个异步操作。|如果句柄上的上一个函数调用返回 SQL_STILL_EXECUTING，如果启用了通知模式， **SQLCompleteAsync**必须在要执行的后处理工作并完成该操作的句柄上调用。|  
|S1118|驱动程序不支持异步通知|当该驱动程序不支持异步通知时，不能设置 SQL_ATTR_ASYNC_DBC_EVENT 或 SQL_ATTR_ASYNC_DBC_RETCODE_PTR。|  
  
## <a name="comments"></a>注释  
 有关原因的信息应用程序使用**SQLConnect**，请参阅[使用 SQLConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)。  
  
 驱动程序管理器在直到应用程序调用一个函数不会连接到的驱动程序 (**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**) 连接到驱动程序。 在该点之前，驱动程序管理器处理其自己的句柄，并且管理连接信息。 当应用程序调用连接函数时，驱动程序管理器检查驱动程序当前是否连接到指定*ConnectionHandle*:  
  
-   如果驱动程序未连接到，驱动程序管理器连接到的驱动程序和调用**SQLAllocHandle**与*HandleType*的 SQL_HANDLE_ENV， **SQLAllocHandle**与*HandleType*的 SQL_HANDLE_DBC， **SQLSetConnectAttr** （如果应用程序指定任何连接属性），以及驱动程序中的连接函数。 驱动程序管理器返回 SQLSTATE IM006 (驱动程序的**SQLSetConnectOption**失败) 和连接函数，如果驱动程序返回的错误的 SQL_SUCCESS_WITH_INFO **SQLSetConnectAttr**。 有关详细信息，请参阅[连接到数据源或驱动程序](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)。  
  
-   如果指定的驱动程序已连接到在*ConnectionHandle*，驱动程序管理器驱动程序中调用仅连接函数。 在这种情况下，该驱动程序必须确保所有连接都属性*ConnectionHandle*维护其当前设置。  
  
-   如果连接到不同驱动程序时，驱动程序管理器调用**SQLFreeHandle**与*HandleType*的 SQL_HANDLE_DBC，然后，如果没有其他驱动程序连接到该环境中，它调用**SQLFreeHandle**与*HandleType*的 SQL_HANDLE_ENV 连接驱动程序中，然后断开连接该驱动程序。 它又执行时驱动程序未连接到相同的操作。  
  
 然后，该驱动程序分配句柄和初始化自身。  
  
 在应用程序调用**SQLDisconnect**，驱动程序管理器调用**SQLDisconnect**驱动程序中。 但是，它不会断开该驱动程序。 这在应用程序重复连接到和从数据源断开连接的内存中保留该驱动程序。 在应用程序调用**SQLFreeHandle**与*HandleType*的 SQL_HANDLE_DBC，驱动程序管理器调用**SQLFreeHandle**与*HandleType*的 SQL_HANDLE_DBC 然后**SQLFreeHandle**与*HandleType*的 SQL_HANDLE_ENV 在驱动程序，然后断开连接驱动程序。  
  
 ODBC 应用程序可以建立多个连接。  
  
## <a name="driver-manager-guidelines"></a>驱动程序管理器准则  
 内容 **ServerName*影响驱动程序管理器和驱动程序如何协同工作来建立与数据源的连接。  
  
-   如果\* *ServerName*包含有效数据源名称，驱动程序管理器中的系统信息查找相应的数据源规范并连接到相关的驱动程序。 驱动程序管理器将传递每**SQLConnect**于驱动程序的自变量。  
  
-   如果找不到数据源名称或*ServerName*是 null 指针，驱动程序管理器查找默认数据源说明，并连接到相关的驱动程序。 驱动程序管理器将传递给该驱动程序*用户名*和*身份验证*以未修改形式的自变量和"默认"为*ServerName*自变量。  
  
-   如果*ServerName*参数为"DEFAULT"，驱动程序管理器查找默认数据源说明，并连接到相关的驱动程序。 驱动程序管理器将传递每**SQLConnect**于驱动程序的自变量。  
  
-   如果找不到数据源名称或*ServerName*为 null 指针，并且数据源说明不存在默认值，则驱动程序管理器返回与 SQLSTATE IM002 SQL_ERROR （数据源名称找不到并且没有默认值指定驱动程序）。  
  
 它已连接到的驱动程序管理器后，驱动程序可以在系统信息中找到其相应的数据源规范并使用规范中的特定于驱动程序的信息来完成其一组所需的连接信息。  
  
 如果数据源的系统信息中指定默认转换库，则该驱动程序连接到它。 可以通过调用连接到不同的翻译库**SQLSetConnectAttr**具有 SQL_ATTR_TRANSLATE_LIB 属性。 转换选项只能指定通过调用**SQLSetConnectAttr**具有 SQL_ATTR_TRANSLATE_OPTION 属性。  
  
 如果驱动程序支持**SQLConnect**，驱动程序的系统信息的驱动程序关键字部分必须包含**ConnectFunctions**与第一个字符的关键字设置为"Y"。  
  
### <a name="connection-pooling"></a>连接池  
 连接池允许应用程序重复使用已创建的连接。 当启用连接池和**SQLConnect**调用时，此驱动程序管理器尝试建立连接使用的是已指派给连接池的环境中的连接池的一部分的连接。 此环境是在池中使用连接的所有应用程序都使用一个共享的环境。  
  
 之前通过调用分配环境启用连接池**SQLSetEnvAttr**设置 SQL_ATTR_CONNECTION_POOLING 为 SQL_CP_ONE_PER_DRIVER （它指定每个驱动程序的一个池的最大值） 或 SQL_CP_ONE_PER_HENV（指定每个环境的一个池最的多）。 **SQLSetEnvAttr**在这种情况下使用调用*EnvironmentHandle*设置为 null，这使得进程级别属性的属性。 如果 SQL_ATTR_CONNECTION_POOLING 设置为 SQL_CP_OFF，禁用连接池。  
  
 在启用连接池后， **SQLAllocHandle**与*HandleType* SQL_HANDLE_ENV 称为分配环境。 此调用所分配的环境是共享的环境，因为在启用连接池。 但是，将使用的环境，不确定直到**SQLAllocHandle**与*HandleType* SQL_HANDLE_DBC 的调用。  
  
 **SQLAllocHandle**与*HandleType* SQL_HANDLE_DBC 称为分配连接。 驱动程序管理器尝试查找与匹配由应用程序设置的环境属性的现有共享的环境。 如果不存在任何此类环境，则会创建一个作为一种隐式*共享的环境*。 如果找到匹配的共享的环境，则环境句柄返回给应用程序和其引用计数会递增。  
  
 但是，将使用的连接不决定直到**SQLConnect**调用。 此时，驱动程序管理器尝试查找现有的连接池中的连接请求的应用程序的条件相匹配。 这些条件包括对的调用中请求的连接选项**SQLConnect** (的值*ServerName*，*用户名*，和*身份验证*关键字) 和任何连接属性设置因为**SQLAllocHandle**与*HandleType* SQL_HANDLE_DBC 的调用。 驱动程序管理器检查这些条件对相应的连接关键字和池中的连接中的属性。 如果找到匹配项，则使用池中的连接。 如果不找到任何匹配项，则被创建新的连接。  
  
 如果 SQL_ATTR_CP_MATCH 环境属性设置为 SQL_CP_STRICT_MATCH，则匹配必须为确切的池中要使用的连接。 如果 SQL_ATTR_CP_MATCH 环境属性设置为 SQL_CP_RELAXED_MATCH，连接选项的调用中**SQLConnect**必须匹配，而不是所有连接属性必须匹配。  
  
 下面的规则适用时连接属性中，由应用程序，然后设置**SQLConnect**被调用时，与池中的连接的连接属性不匹配：  
  
-   如果在之前建立连接，则必须设置连接属性：  
  
     如果 SQL_ATTR_CP_MATCH SQL_CP_STRICT_MATCH，在共用连接的 SQL_ATTR_PACKET_SIZE 必须与由应用程序设置的属性相同。 如果 SQL_CP_RELAXED_MATCH，SQL_ATTR_PACKET_SIZE 的值可以不同。  
  
     SQL_ATTR_LOGIN_VALUE 的值不会影响匹配。  
  
-   如果之前或之后进行连接，则可以设置连接属性：  
  
     如果连接属性尚未设置应用程序，但在池中，设置连接上并且没有默认值中的共用连接的连接属性重新设置为默认值，并声明一个匹配项。 如果没有默认值，已入池的连接不被视为匹配项。  
  
     如果连接属性已设置应用程序，但尚未设置连接上在池中，应用程序池的连接属性更改为该组，并声明匹配项。  
  
     如果连接属性已设置该应用程序，并且还已设置连接上在池中，但这些值不匹配，则使用的应用程序的连接属性的值和声明匹配项。  
  
-   如果驱动程序特定的连接属性的值不相同且 SQL_ATTR_CP_MATCH 设为 SQL_CP_STRICT_MATCH，则不会使用池中连接。  
  
 在应用程序调用**SQLDisconnect**断开连接，连接返回到连接池，并且可供重复使用。  
  
### <a name="optimizing-connection-pooling-performance"></a>优化连接池性能  
 当涉及分布式的事务时，就可以优化连接池使用的性能**SQL_DTC_TRANSITION_COST**，这是 SQLUINTEGER 位掩码。 引用转换的连接属性将值 0 不为零，SQL_ATTR_ENLIST_IN_DTC 的转换，反之亦然。 这是从连接未登记到的分布式事务中登记的分布式事务中，反之亦然。 具体取决于如何驱动程序已实现登记 （设置连接属性 SQL_ATTR_ENLIST_IN_DTC），这些转换可能是昂贵，因此应当避免为了获得最佳性能。  
  
 由驱动程序返回的值包含下列位的任意组合：  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**，当设置，则意味着非零转换零比从非零值转换为另一个非零值 （登记在其下一步的事务中登记先前连接） 贵很多。  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**，当设置，则意味着非零零转换比使用其 SQL_ATTR_ENLIST_IN_DTC 属性已设置为零的连接贵很多。  
  
 没有与连接使用情况之间作出权衡性能。 如果驱动程序指示一个或多个这些转换非常昂贵，驱动程序管理器的连接池进程会响应这通过让更多连接池中。 某些池中的连接是首选用于非事务性，而有些则的事务使用首选分发点。 但是，如果驱动程序指示此转换不非常昂贵，较少的连接可用，可能交替非事务性和事务使用。  
  
 不支持 SQL_ATTR_ENLIST_IN_DTC 的驱动程序需要支持 SQL_DTC_TRANSITION_COST。 对于支持 SQL_ATTR_ENLIST_IN_DTC 但不是 SQL_DTC_TRANSITION_COST 的驱动程序，假定转换不占用大量资源，就像该驱动程序返回此值为 0 （没有设置位）。  
  
 尽管 SQL_DTC_TRANSITION_COST ODBC 3.5，ODBC 2 中引入。*x*因为驱动程序管理器将查询此信息无论驱动程序版本是什么，驱动程序可以还支持它。  
  
### <a name="code-example"></a>代码示例  
 在下面的示例中，应用程序分配环境和连接句柄。 然后，它将连接到具有用户 ID 约翰的销售订单数据源和密码芝麻并处理数据。 完成处理数据后，它从数据源断开连接，并释放句柄。  
  
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
|分配的句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|发现和枚举连接到数据源所需值|[SQLBrowseConnect 函数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|从数据源断开连接|[SQLDisconnect 函数](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|连接到使用连接字符串或对话框中的数据源|[SQLDriverConnect 函数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|返回连接属性的设置|[SQLGetConnectAttr 函数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|将连接属性设置|[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)

