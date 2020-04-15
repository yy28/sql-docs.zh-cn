---
title: SQLConnect 功能 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ab0a31845efeb484c554a9c9cf1afeaeab1a8bea
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301213"
---
# <a name="sqlconnect-function"></a>SQLConnect 函数
**一致性**  
 推出版本： ODBC 1.0 标准合规性： ISO 92  
  
 **摘要**  
 **SQLConnect**建立与驱动程序和数据源的连接。 连接句柄引用有关数据源连接的所有信息的存储，包括状态、事务状态和错误信息。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
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
 *连接句柄*  
 [输入] 连接句柄。  
  
 *ServerName*  
 [输入]数据源名称。 数据可能位于与程序相同的计算机上，或者位于网络上的另一台计算机上。 有关应用程序如何选择数据源的信息，请参阅[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 *NameLength1*  
 [输入]长度 = 以字符表示*服务器名称*。  
  
 *用户*  
 [输入]用户标识符。  
  
 *名称长度2*  
 [输入]长度 =*字符中的用户名*。  
  
 *身份验证*  
 [输入]身份验证字符串（通常是密码）。  
  
 *名称长度3*  
 [输入]长度 =*字符身份验证*。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE 或SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLConnect**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，可以通过调用**SQLGetDiagRec**获取关联的 SQLSTATE 值，该值具有SQL_HANDLE_DBC的*句柄类型*和*连接句柄*的*句柄*。 下表列出了**SQLConnect**通常返回的 SQLSTATE 值，并在此函数的上下文中解释每个值;符号"（DM）"在驱动程序管理器返回的 SQLStatEs 描述之前。 除非另有说明，否则与每个 SQLSTATE 值关联的返回代码将SQL_ERROR。  
  
|SQLSTATE|错误|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定于驱动程序的信息消息。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|01S02|选项值已更改|驱动程序不支持**SQLSetConnectAttr**中*ValuePtr*参数的指定值，并替换了类似的值。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|08001|客户端无法建立连接|驱动程序无法与数据源建立连接。|  
|08002|正在使用的连接名称|（DM） 指定的*ConnectHandle*已用于与数据源建立连接，并且连接仍处于打开状态或用户正在浏览连接。|  
|08004|服务器拒绝连接|数据源出于实现定义的原因拒绝建立连接。|  
|08S01|通信链路故障|在函数完成处理之前，驱动程序与驱动程序尝试连接到的数据源之间的通信链路失败。|  
|28000|无效的授权规范|为参数*UserName*指定的值或为参数指定的值*身份验证*违反了数据源定义的限制。|  
|HY000|常规错误|发生一个错误，其中没有特定的 SQLSTATE，并且没有定义特定于实现的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*缓冲区中返回的错误消息描述了错误及其原因。|  
|HY001|内存分配错误|（DM） 驱动程序管理器无法分配支持执行或完成函数所需的内存。|  
|HY008|操作已取消|为*连接句柄*启用了异步处理。 SQLConnect 函数被调用，在完成执行之前，在 ConnectHandle 上调用[了 SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)，然后在**SQLConnect** *ConnectHandle*上再次调用**SQLConnect**函数。 *ConnectionHandle*<br /><br /> 或者 **，SQLConnect**函数被调用，在完成执行之前 **，SQLCancelHandle**是从多线程应用程序中的不同线程调用的*ConnectHandle。*|  
|HY010|函数序列错误|（DM） 为*ConnectHandle*调用了异步执行函数（不是此函数），并且在调用此函数时仍在执行。|  
|HY013|内存管理错误|无法处理函数调用，因为无法访问基础内存对象，可能是因为内存条件较低。|  
|HY090|无效的字符串或缓冲区长度|（DM） 为参数*NameLength1、NameLength2*或*NameLength3*指定的值小于 0，但不等于SQL_NTS。 *NameLength2*<br /><br /> （DM） 为参数*NameLength1*指定的值超过了数据源名称的最大长度。|  
|HYT00|超时时间已到|查询超时期限在连接到数据源之前过期。 超时期间通过**SQLSetConnectAttr**SQL_ATTR_LOGIN_TIMEOUT设置。|  
|HY114|驱动程序不支持连接级异步功能执行|（DM） 在进行连接之前，应用程序在连接句柄上启用了异步操作。 但是，驱动程序不支持对连接句柄的异步操作。|  
|HYT01|连接超时已过期|在数据源响应请求之前，连接超时期限已过期。 连接超时周期通过**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT设置。|  
|IM001|驱动程序不支持此功能|（DM） 数据源名称指定的驱动程序不支持该函数。|  
|IM002|找不到数据源，未指定默认驱动程序|（DM） 参数*ServerName*中指定的数据源名称未在系统信息中找到，也没有默认驱动程序规范。|  
|IM003|指定的驱动程序无法连接到|（DM） 由于其他原因，找不到或无法连接到系统信息中的数据源规范中列出的驱动程序。|  
|IM004|驱动程序的 SQLAllocHandle 上SQL_HANDLE_ENV失败|（DM） 在**SQLConnect**期间，驱动程序管理器调用驱动程序的**SQLAllocHandle**函数，该函数具有SQL_HANDLE_ENV的*句柄类型*，驱动程序返回了错误。|  
|IM005|驱动程序的 SQLAllocHandle 上SQL_HANDLE_DBC失败|（DM） 在**SQLConnect**期间，驱动程序管理器调用驱动程序的**SQLAllocHandle**函数，该*函数具有SQL_HANDLE_DBC的句柄类型*，驱动程序返回了错误。|  
|IM006|驱动程序的 SQLSetConnectAttr 失败|在**SQLConnect**期间，驱动程序管理器调用驱动程序的**SQLSetConnectAttr**函数，驱动程序返回了错误。 （函数返回SQL_SUCCESS_WITH_INFO。|  
|IM009|无法连接到翻译 DLL|驱动程序无法连接到为数据源指定的转换 DLL。|  
|IM010|数据源名称太长|（DM）*\*服务器名称*长于SQL_MAX_DSN_LENGTH个字符。|  
|IM014|指定的 DSN 包含驱动程序和应用程序之间的体系结构不匹配|（DM） 32 位应用程序使用 DSN 连接到 64 位驱动程序;反之亦然。|  
|IM015|驱动程序的 SQLConnect SQL_HANDLE_DBC_INFO_HANDLE发生故障|如果驱动程序返回SQL_ERROR，驱动程序管理器将返回SQL_ERROR到应用程序，连接将失败。<br /><br /> 有关SQL_HANDLE_DBC_INFO_TOKEN的详细信息，请参阅在[ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。|  
|IM017|在异步通知模式下禁用轮询|每当使用通知模型时，都会禁用轮询。|  
|IM018|尚未调用**SQLCompleteAsync**以完成对此句柄的先前异步操作。|如果句柄上的上一个函数调用返回SQL_STILL_EXECUTING，并且启用了通知模式，则必须在句柄上调用**SQLCompleteAsync**以执行后处理并完成操作。|  
|S1118|驱动程序不支持异步通知|当驱动程序不支持异步通知时，无法设置SQL_ATTR_ASYNC_DBC_EVENT或SQL_ATTR_ASYNC_DBC_RETCODE_PTR。|  
  
## <a name="comments"></a>注释  
 有关应用程序使用**SQLConnect**的原因的信息，请参阅[与 SQLConnect 连接](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)。  
  
 驱动程序管理器不会连接到驱动程序，直到应用程序调用函数 **（SQLConnect，** **SQLDriverConnect**， 或**SQLBrowseConnect**） 连接到驱动程序. 在此之前，驱动程序管理器使用其自己的句柄并管理连接信息。 当应用程序调用连接函数时，驱动程序管理器检查驱动程序当前是否连接到指定的*ConnectHandle*：  
  
-   如果驱动程序未连接到，驱动程序管理器连接到驱动程序，并且调用**SQLAllocHandle**与 SQL_HANDLE_ENV 的*句柄类型*、具有*SQL_HANDLE_DBC句柄类型的*SQLAllocHandle、SQLSetConnectAttr（如果应用程序指定任何连接属性）和驱动程序中的连接功能。 **SQLAllocHandle** **SQLSetConnectAttr** 如果驱动程序返回**SQLSetConnectAttr**的错误，驱动程序管理器将返回 SQLSTATE IM006（驱动程序的**SQLSetConnectOption**失败）和连接函数SQL_SUCCESS_WITH_INFO。 有关详细信息，请参阅[连接到数据源或驱动程序](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)。  
  
-   如果指定的驱动程序已连接到*ConnectHandle*上，则驱动程序管理器仅调用驱动程序中的连接功能。 在这种情况下，驱动程序必须确保*ConnectHandle*的所有连接属性都保持其当前设置。  
  
-   如果连接到其他驱动程序，驱动程序管理器将**SQLFreeHandle**调用具有 SQL_HANDLE_DBC 的*句柄类型*，然后，如果该环境中没有其他驱动程序连接到**SQLFreeHandle，则调用 SQLFreeHandle，** 在连接的驱动程序中使用 SQL_HANDLE_ENV的*句柄类型*，然后断开该驱动程序。 然后，它执行与驱动程序未连接到时相同的操作。  
  
 然后，驱动程序分配句柄并初始化自身。  
  
 当应用程序调用**SQLDISCONNECT**时，驱动程序管理器在驱动程序中调用**SQLDISCONNECT。** 但是，它不会断开驱动程序。 这样，对于反复连接到数据源并断开与数据源的连接的应用程序，驱动程序将保留在内存中。 当应用程序使用*SQL_HANDLE_DBC的句柄类型*调用**SQLFreeHandle**时，驱动程序管理器使用SQL_HANDLE_DBC*的句柄类型*调用**SQLFreeHandle，** 然后在驱动程序中使用 SQL_HANDLE_ENV的*句柄类型*调用**SQLFreeHandle，** 然后断开驱动程序的连接。  
  
 ODBC 应用程序可以建立多个连接。  
  
## <a name="driver-manager-guidelines"></a>驾驶员经理指南  
 **ServerName*的内容会影响驱动程序管理器和驱动程序协同工作以建立与数据源的连接的方式。  
  
-   如果\* *ServerName*包含有效的数据源名称，驱动程序管理器将查找系统信息中的相应数据源规范并连接到关联的驱动程序。 驱动程序管理器将每个**SQLConnect**参数传递给驱动程序。  
  
-   如果找不到数据源名称或*ServerName*是空指针，驱动程序管理器将查找默认数据源规范并连接到关联的驱动程序。 驱动程序管理器将*未修改的用户名*和*身份验证*参数传递给驱动程序，将*服务器名称*参数的"DEFAULT"传递给驱动程序。  
  
-   如果*服务器名称*参数为"DEFAULT"，驱动程序管理器将查找默认数据源规范并连接到关联的驱动程序。 驱动程序管理器将每个**SQLConnect**参数传递给驱动程序。  
  
-   如果找不到数据源名称或*ServerName*是空指针，并且默认数据源规范不存在，则驱动程序管理器将返回 SQL_ERROR SQLSTATE IM002（找不到数据源名称，未指定默认驱动程序）。  
  
 驱动程序管理器连接到它后，驱动程序可以在系统信息中查找其相应的数据源规范，并使用规范中的特定于驱动程序的信息来完成其所需的连接信息集。  
  
 如果在数据源的系统信息中指定了默认翻译库，则驱动程序将连接到该库。 使用SQL_ATTR_TRANSLATE_LIB属性调用**SQLSetConnectAttr，** 可以连接到不同的翻译库。 可以通过使用SQL_ATTR_TRANSLATE_OPTION属性调用**SQLSetConnectAttr**来指定转换选项。  
  
 如果驱动程序支持**SQLConnect，** 则驱动程序的系统信息的驱动程序关键字部分必须包含**ConnectFunctions**关键字，第一个字符设置为"Y"。  
  
### <a name="connection-pooling"></a>连接池  
 连接池允许应用程序重用已创建的连接。 启用连接池并调用**SQLConnect**时，驱动程序管理器尝试使用已指定用于连接池的环境中的连接池的一部分进行连接。 此环境是一个共享环境，由使用池中连接的所有应用程序使用。  
  
 在分配环境之前，通过调用**SQLSetEnvAttr**将SQL_ATTR_CONNECTION_POOLING设置为SQL_CP_ONE_PER_DRIVER（每个驱动程序最多指定一个池）或SQL_CP_ONE_PER_HENV（每个环境最多指定一个池）。在分配环境之前启用连接池。 在这种情况下 **，SQLSetEnvAttr**调用*环境处理设置为*null，这使得属性成为进程级属性。 如果SQL_ATTR_CONNECTION_POOLING设置为SQL_CP_OFF，则禁用连接池。  
  
 启用连接池后，将调用具有*句柄类型*SQL_HANDLE_ENV **SQLAllocHandle**来分配环境。 此调用分配的环境是共享环境，因为连接池已启用。 但是，在调用具有SQL_HANDLE_DBC的**SQLAllocHandle**之前，不会确定将使用*HandleType*的环境。  
  
 调用具有*处理类型*SQL_HANDLE_DBC的**SQLAllocHandle**来分配连接。 驱动程序管理器尝试查找与应用程序设置的环境属性匹配的现有共享环境。 如果不存在此类环境，则创建一个环境作为隐式*共享环境*。 如果找到匹配的共享环境，环境句柄将返回到应用程序，其引用计数将递增。  
  
 但是，在调用**SQLConnect**之前，不会确定将使用的连接。 此时，驱动程序管理器尝试在连接池中找到与应用程序请求的条件匹配的现有连接。 这些标准包括在调用**SQLConnect**时请求的连接选项（*服务器名称*、*用户名*和*身份验证*关键字的值）以及自调用具有*SQL_HANDLE_DBC的***SQLAllocHandle**以来设置的任何连接属性。 驱动程序管理器根据池中连接中的相应连接关键字和属性检查这些标准。 如果找到匹配项，则使用池中的连接。 如果未找到匹配项，则创建新连接。  
  
 如果SQL_ATTR_CP_MATCH环境属性设置为SQL_CP_STRICT_MATCH，则使用池中的连接必须精确匹配。 如果将SQL_ATTR_CP_MATCH环境属性设置为SQL_CP_RELAXED_MATCH，则调用**SQLConnect**中的连接选项必须匹配，但不是所有连接属性必须匹配。  
  
 当调用**SQLConnect**之前由应用程序设置的连接属性与池中连接的连接属性不匹配时，将应用以下规则：  
  
-   如果在建立连接之前必须设置连接属性：  
  
     如果SQL_CP_STRICT_MATCHSQL_ATTR_CP_MATCH，则池连接中的SQL_ATTR_PACKET_SIZE必须与应用程序设置的属性相同。 如果SQL_CP_RELAXED_MATCH，则SQL_ATTR_PACKET_SIZE的值可能不同。  
  
     SQL_ATTR_LOGIN_VALUE的值不会影响匹配。  
  
-   如果在建立连接之前或之后可以设置连接属性：  
  
     如果连接属性尚未由应用程序设置，但已在池中的连接上设置，并且存在默认值，则池连接中的连接属性将设置回默认值并声明匹配。 如果没有默认值，则池连接不被视为匹配。  
  
     如果连接属性已由应用程序设置，但尚未在池中的连接上设置，则池上的连接属性将由应用程序更改为该集，并声明匹配项。  
  
     如果连接属性已由应用程序设置，并且也已在池中的连接上设置，但值不同，则使用应用程序的连接属性的值并声明匹配项。  
  
-   如果特定于驱动程序的连接属性的值不相同，并且SQL_ATTR_CP_MATCH设置为SQL_CP_STRICT_MATCH，则不使用池中的连接。  
  
 当应用程序调用**SQLDisconnect**断开连接时，连接将返回到连接池，可供重用。  
  
### <a name="optimizing-connection-pooling-performance"></a>优化连接池性能  
 当涉及分布式事务时，可以使用**SQL_DTC_TRANSITION_COST**来优化连接池性能，这是 SQLUINTEGER 位掩码。 引用的过渡是连接属性SQL_ATTR_ENLIST_IN_DTC从值 0 到非零的过渡，反之亦然。 这是一个连接，从未在分布式事务中登记到在分布式事务中登记，反之亦然。 根据驱动程序如何实现登记（设置连接属性SQL_ATTR_ENLIST_IN_DTC），这些转换可能非常昂贵，因此应避免进行，以获得最佳性能。  
  
 驱动程序返回的值包含以下位的任意组合：  
  
-   **SQL_DTC_ENLIST_EXPENSIVE**，设置时，意味着零到非零转换比从非零转换到另一个非零值（在其下一个事务中登记以前登记的连接）要昂贵得多。  
  
-   **SQL_DTC_UNENLIST_EXPENSIVE**设置时，意味着非零到零转换比使用SQL_ATTR_ENLIST_IN_DTC属性已设置为零的连接要昂贵得多。  
  
 性能与连接使用权衡。 如果驱动程序指示其中一个或多个转换成本高昂，则驱动程序管理器的连接池管理器通过在池中保留更多连接来响应此。 池中的某些连接是非事务用途的首选，有些连接是事务用途的首选。 但是，如果驱动程序指示这些转换不昂贵，则可以使用较少的连接，也许在非事务性和事务性使用之间交替使用。  
  
 不支持SQL_ATTR_ENLIST_IN_DTC的驱动程序不需要支持SQL_DTC_TRANSITION_COST。 对于支持SQL_ATTR_ENLIST_IN_DTC但不SQL_DTC_TRANSITION_COST的驱动程序，假定转换并不昂贵，就像驱动程序为此值返回 0（未设置位）。  
  
 虽然在 ODBC 3.5 中引入了SQL_DTC_TRANSITION_COST，但 ODBC 2。*x*驱动程序也可以支持它，因为驱动程序管理器将查询此信息，而不考虑驱动程序版本。  
  
### <a name="code-example"></a>代码示例  
 在下面的示例中，应用程序分配环境和连接句柄。 然后，它使用用户 ID JohnS 和密码芝麻连接到 SalesOrders 数据源并处理数据。 处理完数据后，它将断开数据源的连接并释放句柄。  
  
```cpp  
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
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|分配句柄|[SQLAllocHandle 函数](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|发现和枚举连接到数据源所需的值|[SQLBrowseConnect 函数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|与数据源断开连接|[SQLDisconnect 函数](../../../odbc/reference/syntax/sqldisconnect-function.md)|  
|使用连接字符串或对话框连接到数据源|[SQLDriverConnect 函数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|返回连接属性的设置|[SQLGetConnectAttr 函数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|设置连接属性|[SQLSetConnectAttr 函数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
