---
title: SQLManageDataSources | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLManageDataSources
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLManageDataSources
helpviewer_keywords:
- SQLManageDataSources [ODBC]
ms.assetid: ac6d186f-b394-406c-94c4-c6331d1ca468
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 529c503bc10d3ed0b69a4c280c7fa63e72893f8f
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536568"
---
# <a name="sqlmanagedatasources"></a>SQLManageDataSources
**符合性**  
 版本引入了：ODBC 2.0  
  
 **摘要**  
 **SQLManageDataSources**显示一个对话框，可使用该用户可以设置、 添加和删除数据源中的系统信息。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLManageDataSources(  
     HWND     hwnd);  
```  
  
## <a name="arguments"></a>参数  
 *hwnd*  
 [输入]父窗口句柄。  
  
## <a name="returns"></a>返回  
 **SQLManageDataSources**如果，则返回*hwnd*不是有效的窗口句柄。 否则，返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLManageDataSources**返回 FALSE，关联 *\*pfErrorCode*可以通过调用获取的值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|出错的其中没有特定的安装程序错误。|  
|ODBC_ERROR_REQUEST_FAILED|*请求*失败|在调用**ConfigDSN**失败。|  
|ODBC_ERROR_INVALID__HWND|窗口句柄无效|*Hwnd*参数为无效或为 NULL。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="managing-data-sources"></a>管理数据源  
 **SQLManageDataSources**最初会显示**ODBC 数据源管理器**对话框，如以下插图所示。  
  
 ![ODBC 数据源管理器对话框](../../../odbc/reference/syntax/media/ch23e.gif "CH23E")  
  
 该对话框中显示三个选项卡下的系统信息中列出的数据源：**用户 DSN**，**系统 DSN**，和**文件 DSN**。 如果用户双击数据源或选择数据源并单击**配置**， **SQLManageDataSources**调用**ConfigDSN**设置 ODBC_CONFIG_ 与 DLL 中DSN 选项。  
  
 如果用户单击**外**， **SQLManageDataSources**显示**创建新的数据源**对话框中，如下图中所示。  
  
 ![创建新数据源对话框](../../../odbc/reference/syntax/media/ch23f.gif "CH23F")  
  
 对话框的显示安装的驱动程序的列表。 如果用户双击驱动程序或选择一个驱动程序并单击**确定**， **SQLManageDataSources**调用**ConfigDSN**中安装程序 DLL 并将其传递 ODBC_ADD_DSN 选项。  
  
 如果用户选择数据源并单击**删除**， **SQLManageDataSources**询问用户是否要删除数据源。 如果用户单击**是**， **SQLManageDataSources**调用**ConfigDSN** ODBC_REMOVE_DSN 选项与安装程序 DLL 中。  
  
 **创建新的数据源**对话框用于添加或删除用户数据源、 系统数据源或文件数据源。  
  
## <a name="user-dsns"></a>用户 Dsn  
 为单个用户创建的 Dsn 将调用用户 Dsn，以区别于系统 Dsn。 用户 Dsn 的系统信息中注册，如下所示：  
  
 `HKEY_CURRENT_USERS`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbc.ini`  
  
## <a name="system-dsns"></a>系统 Dsn  
 **创建新的数据源**对话框允许您将系统数据源添加到你的本地计算机或删除一个，或系统数据源的配置设置。  
  
 可以通过同一台计算机上的多个用户使用数据源设置的系统数据源名称 (DSN)。 它还可以使用由系统级服务，即使没有用户登录到计算机，然后可以获得对数据源的访问。  
  
 系统 DSN 的系统信息中，而不是在 HKEY_CURRENT_USER 项中的 HKEY_LOCAL_MACHINE 项中注册。 它位于未与某位用户使用其自己特定的用户名和密码登录，但可以使用该计算机的任何用户或者自动系统级服务。 系统 DSN，但是，与一台计算机。 它不支持使用远程计算机之间的 Dsn 的功能。 系统 Dsn 的系统信息中注册，如下所示：  
  
 HKEY_LOCAL_MACHINE    SOFTWARE       ODBC          Odbc.ini  
  
## <a name="file-dsns"></a>文件 Dsn  
 文件数据源没有数据源名称，如计算机数据源，不会和未注册到任何一个用户或计算机。 可以将复制到任何计算机.dsn 文件中包含该数据源的连接信息。 文件数据源可以是可共享，在这种情况下.dsn 文件驻留在网络上，并可由同时在网络上的多个用户，只要用户具有适当的驱动程序。 文件数据源还可以共享，在这种情况下可以使用仅在一台计算机上。  
  
 文件数据源的详细信息，请参阅[连接使用的文件数据源](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)，或请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
## <a name="managing-drivers"></a>管理驱动程序  
 如果用户单击**驱动程序**选项卡**ODBC 数据源管理器**对话框中， **SQLManageDataSources**显示在系统上，安装 ODBC 驱动程序的列表以及驱动程序有关的信息。 下图中所示，显示的日期是该驱动程序的创建日期。  
  
 ![ODBC 数据源管理器驱动程序选项卡](../../../odbc/reference/syntax/media/ch23g.gif "ch23g")  
  
## <a name="tracing-options"></a>跟踪选项  
 如果用户单击**跟踪**选项卡**ODBC 数据源管理器**对话框中， **SQLManageDataSources**显示跟踪选项，在下面的示例所示图。  
  
 ![ODBC 数据源管理器跟踪选项卡](../../../odbc/reference/syntax/media/ch23h.gif "Ch23h")  
  
 如果用户单击**立即开始跟踪**，然后单击**确定**， **SQLManageDataSources**手动为在计算机上当前正在运行的所有应用程序启用跟踪。  
  
 如果用户指定的跟踪文件中的名称**日志文件路径**文本框中，然后单击**确定**， **SQLManageDataSources**设置**TraceFile**为指定的名称的系统信息 [ODBC] 部分中的关键字。  
  
> [!IMPORTANT]  
>  在 Windows 8 中 （Visual Studio 分析器仅包含在较旧版本的 Visual Studio。） 开始已不再对 Visual Studio 分析器的支持。 有关故障排除机制的替代方法，使用 BID 跟踪。  
  
 如果用户单击**启动 Visual Studio 分析器**，然后单击**确定**，启用 Visual Studio 分析器。 它将保持启用状态，直到**停止 Visual Studio 分析器**单击。  
  
 有关跟踪的详细信息，请参阅[跟踪](../../../odbc/reference/develop-app/tracing.md)。 有关详细信息**跟踪**并**TraceFile**关键字，请参见[ODBC 子项](../../../odbc/reference/install/odbc-subkey.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|创建数据源|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|
