---
title: "SQLManageDataSources |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLManageDataSources
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLManageDataSources
helpviewer_keywords: SQLManageDataSources [ODBC]
ms.assetid: ac6d186f-b394-406c-94c4-c6331d1ca468
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8bfd528a3b401cdae956701c8934c2333e01109d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sqlmanagedatasources"></a>SQLManageDataSources
**一致性**  
 版本引入了： ODBC 2.0  
  
 **摘要**  
 **SQLManageDataSources**显示一个对话框，可与该用户可以设置、 添加和删除数据源中的系统信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL SQLManageDataSources(  
     HWND     hwnd);  
```  
  
## <a name="arguments"></a>参数  
 *hwnd*  
 [输入]父窗口句柄。  
  
## <a name="returns"></a>返回  
 **SQLManageDataSources**如果返回 FALSE *hwnd*不是有效的窗口句柄。 否则，它将返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLManageDataSources**返回 FALSE，一个关联 *\*pfErrorCode*可通过调用获取值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError**并解释此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|对于发生了错误其中没有任何特定的安装程序错误。|  
|ODBC_ERROR_REQUEST_FAILED|*请求*失败|调用**ConfigDSN**失败。|  
|ODBC_ERROR_INVALID__HWND|窗口句柄无效|*Hwnd*自变量为无效或为空。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="managing-data-sources"></a>管理数据源  
 **SQLManageDataSources**最初显示**ODBC 数据源管理器**对话框中，如下面的插图中所示。  
  
 ![ODBC 数据源管理器对话框](../../../odbc/reference/syntax/media/ch23e.gif "CH23E")  
  
 对话框中显示三个选项卡下的系统信息中列出的数据源：**用户 DSN**，**系统 DSN**，和**文件 DSN**。 如果用户双击数据源或选择数据源并单击**配置**， **SQLManageDataSources**调用**ConfigDSN**在安装程序与 ODBC_CONFIG_ DLLDSN 选项。  
  
 如果用户单击**添加**， **SQLManageDataSources**显示**新建数据源**对话框中，如下图所示。  
  
 ![创建新的数据源对话框](../../../odbc/reference/syntax/media/ch23f.gif "CH23F")  
  
 对话框中显示已安装的驱动程序的列表。 如果用户双击驱动程序或选择驱动程序并单击**确定**， **SQLManageDataSources**调用**ConfigDSN**安装程序 DLL 中并将其传递 ODBC_ADD_DSN 选项。  
  
 如果用户选择数据源并单击**删除**， **SQLManageDataSources**询问用户是否要删除数据源。 如果用户单击**是**， **SQLManageDataSources**调用**ConfigDSN** ODBC_REMOVE_DSN 选项与安装程序 DLL 中。  
  
 **新建数据源**对话框用于添加或删除用户数据源、 系统数据源或文件数据源。  
  
## <a name="user-dsns"></a>用户 Dsn  
 为单个用户创建的 Dsn 将会调用用户 Dsn，以区别于系统 Dsn。 用户 Dsn 的系统信息中注册，如下所示：  
  
 `HKEY_CURRENT_USERS`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbc.ini`  
  
## <a name="system-dsns"></a>系统 Dsn  
 **新建数据源**对话框中，你将系统数据源添加到本地计算机或删除一个，或设置的系统数据源的配置。  
  
 数据源使用系统数据源名称 (DSN) 设置可由同一台计算机上的多个用户。 它还可以使用由系统级服务，即使没有用户登录到计算机，然后可以获得对数据源的访问。  
  
 系统 DSN 已注册的系统信息中而不是在 HKEY_CURRENT_USER 项中的 HKEY_LOCAL_MACHINE 项中。 它位于未与某位用户登录时使用他或她特定用户名和密码，但可以使用由该计算机的任何用户或自动系统级服务。 系统 DSN，但是，与一台计算机。 它不支持使用远程 Dsn 机之间的功能。 系统 Dsn 的系统信息中注册，如下所示：  
  
 HKEY_LOCAL_MACHINE 软件 ODBC Odbc.ini  
  
## <a name="file-dsns"></a>文件 Dsn  
 文件数据源没有数据源名称，不机器数据源，以及未注册到任何一个用户或计算机。 可以复制到任何计算机的.dsn 文件中包含该数据源的连接信息。 文件数据源可以是可共享，在这种情况下.dsn 文件驻留在网络上，并可同时使用将由网络上的多个用户，只要用户具有适当的驱动程序。 文件数据源也可以共享，在这种情况下可以使用仅在一台计算机上。  
  
 文件数据源的详细信息，请参阅[连接使用的文件数据源](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)，或请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
## <a name="managing-drivers"></a>管理驱动程序  
 如果用户单击**驱动程序**选项卡中**ODBC 数据源管理器**对话框中， **SQLManageDataSources**显示在系统上，安装的 ODBC 驱动程序的列表以及有关的驱动程序的信息。 下图中所示，所显示的日期是该驱动程序，创建日期。  
  
 ![ODBC 数据源管理器驱动程序选项卡](../../../odbc/reference/syntax/media/ch23g.gif "ch23g")  
  
## <a name="tracing-options"></a>跟踪选项  
 如果用户单击**跟踪**选项卡中**ODBC 数据源管理器**对话框中， **SQLManageDataSources**显示跟踪选项，如在下面的示例所示图。  
  
 ![ODBC 数据源管理器跟踪选项卡](../../../odbc/reference/syntax/media/ch23h.gif "Ch23h")  
  
 如果用户单击**立即开始跟踪**，然后单击**确定**， **SQLManageDataSources**手动为在计算机上当前运行的所有应用程序启用跟踪。  
  
 如果用户指定的名称中的跟踪文件**日志文件路径**文本框中，然后单击**确定**， **SQLManageDataSources**设置**TraceFile**为指定名称的系统信息 [ODBC] 部分中的关键字。  
  
> [!IMPORTANT]  
>  Windows 8 （Visual Studio Analyzer 仅包含在较旧版本的 Visual Studio。） 从开始已删除的 Visual Studio Analyzer 的支持。 有关故障排除机制的替代方法，使用 BID 跟踪。  
  
 如果用户单击**启动 Visual Studio Analyzer** ，然后单击**确定**，启用 Visual Studio 分析器。 它将保持启用状态，直到**停止 Visual Studio Analyzer**单击。  
  
 有关跟踪的详细信息，请参阅[跟踪](../../../odbc/reference/develop-app/tracing.md)。 有关详细信息**跟踪**和**TraceFile**关键字，请参阅[ODBC 子项](../../../odbc/reference/install/odbc-subkey.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|创建数据源|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|
