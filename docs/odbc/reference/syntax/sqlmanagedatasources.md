---
title: SQL管理数据源 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b572a861af3479e1543be9fda9598cc7e25d36c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290208"
---
# <a name="sqlmanagedatasources"></a>SQLManageDataSources
**一致性**  
 版本介绍： ODBC 2.0  
  
 **摘要**  
 **SQLManageDataSources**显示一个对话框，用户可以使用该对话框在系统信息中设置、添加和删除数据源。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLManageDataSources(  
     HWND     hwnd);  
```  
  
## <a name="arguments"></a>参数  
 *霍恩德*  
 [输入]父窗口句柄。  
  
## <a name="returns"></a>返回  
 如果*hwnd*不是有效的窗口句柄 **，SQLManageData 源**将返回 FALSE。 否则，返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLManageDataSources**返回 FALSE 时，可以通过调用**SQL 安装程序获取**关联的*\*pfErrorCode*值。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|发生没有特定安装程序错误的错误。|  
|ODBC_ERROR_REQUEST_FAILED|*请求*失败|对**ConfigDSN 的**调用失败。|  
|ODBC_ERROR_INVALID__HWND|无效的窗口句柄|*hwnd*参数无效或 NULL。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该功能。|  
  
## <a name="managing-data-sources"></a>管理数据源  
 **SQLManageDataSource**最初显示**ODBC 数据源管理员**对话框，如下图所示。  
  
 ![“ODBC 数据源管理器”对话框](../../../odbc/reference/syntax/media/ch23e.gif "CH23E")  
  
 该对话框在三个选项卡下显示系统信息中列出的数据源：**用户 DSN、** 系统**DSN**和**文件 DSN**。 如果用户双击数据源或选择数据源并单击"**配置****"，SQLManageDataSource**在设置 DLL 中调用**ConfigDSN，** 并带有ODBC_CONFIG_DSN选项。  
  
 如果用户单击"**添加** **"，SQLManageDataSources**将显示 **"创建新数据源"** 对话框，如下图所示。  
  
 ![“创建新数据源”对话框](../../../odbc/reference/syntax/media/ch23f.gif "CH23F")  
  
 该对话框显示已安装驱动程序的列表。 如果用户双击驱动程序或选择驱动程序并单击 **"确定****"，SQLManageDataSources**在设置 DLL 中调用**ConfigDSN**并传递ODBC_ADD_DSN选项。  
  
 如果用户选择数据源并单击 **"删除****"，SQLManageDataSource**会询问用户是否要删除数据源。 如果用户单击"**是****"，SQLManageDataSources**在设置 DLL 中调用**ConfigDSN，** 并带有ODBC_REMOVE_DSN选项。  
  
 **"创建新数据源"** 对话框用于添加或删除用户数据源、系统数据源或文件数据源。  
  
## <a name="user-dsns"></a>用户 DSN  
 为单个用户创建的 DSN 将称为用户 DSN，以将其与系统 DSN 区分开来。 用户 DSN 在系统信息中注册如下：  
  
 `HKEY_CURRENT_USERS`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbc.ini`  
  
## <a name="system-dsns"></a>系统 DSN  
 **"创建新数据源"** 对话框允许您向本地计算机添加系统数据源或删除一个，或设置系统数据源的配置。  
  
 使用系统数据源名称 （DSN） 设置的数据源可以由同一台计算机上的多个用户使用。 它也可以由系统范围的服务使用，然后即使没有用户登录到计算机，该服务也可以访问数据源。  
  
 系统 DSN 在系统信息HKEY_LOCAL_MACHINE条目中注册，而不是在HKEY_CURRENT_USER条目中注册。 它不绑定到使用其特定用户名和密码登录的用户，但该计算机的任何用户或自动系统范围的服务都可以使用。 但是，系统 DSN 与一台计算机绑定。 它不支持在计算机之间使用远程 DSN 的功能。 系统 DSN 在系统信息中注册如下：  
  
 HKEY_LOCAL_MACHINE 软件 ODBC Odbc.ini  
  
## <a name="file-dsns"></a>文件 DSN  
 文件数据源没有数据源名称，计算机数据源也是如此，并且不注册给任何一个用户或计算机。 该数据源的连接信息包含在可以复制到任何计算机的 .dsn 文件中。 文件数据源可以共享，在这种情况下，.dsn 文件驻留在网络上，并且只要用户安装了适当的驱动程序，就可以由网络上的多个用户同时使用。 文件数据源也可以不可共享，在这种情况下，它只能在一台计算机上使用。  
  
 有关文件数据源的详细信息，请参阅[使用文件数据源进行连接](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)，或请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
## <a name="managing-drivers"></a>管理驱动程序  
 如果用户单击**ODBC 数据源管理员**对话框中的 **"驱动程序"** 选项卡 **，SQLManageDataSource**将显示系统上安装的 ODBC 驱动程序的列表以及有关驱动程序的信息。 显示的日期是驱动程序的创建日期，如下图所示。  
  
 ![“ODBC 数据源管理器驱动程序”选项卡](../../../odbc/reference/syntax/media/ch23g.gif "ch23g")  
  
## <a name="tracing-options"></a>跟踪选项  
 如果用户单击**ODBC 数据源管理员**对话框中的 **"跟踪"** 选项卡 **，SQLManageDataSources**将显示跟踪选项，如下图所示。  
  
 ![“ODBC 数据源管理器跟踪”选项卡](../../../odbc/reference/syntax/media/ch23h.gif "Ch23h")  
  
 如果用户单击"**立即开始跟踪"，** 然后单击"**确定****"，SQLManageDataSources**可手动跟踪计算机上当前运行的所有应用程序。  
  
 如果用户在**日志文件 Path**文本框中指定跟踪文件的名称，然后单击 **"确定****"，SQLManageDataSources**将系统信息 [ODBC] 部分中的**TraceFile**关键字设置为指定的名称。  
  
> [!IMPORTANT]  
>  从 Windows 8 开始删除了对可视化工作室分析器的支持（视觉工作室分析器仅包含在旧版本的 Visual Studio 中）。 对于其他故障排除机制，请使用 BID 跟踪。  
  
 如果用户单击"**开始视觉工作室分析器**"，然后单击"**确定**"，则启用了可视化工作室分析器。 在单击**停止可视化工作室分析器**之前，它将保持启用状态。  
  
 有关跟踪的详细信息，请参阅[跟踪](../../../odbc/reference/develop-app/tracing.md)。 有关**跟踪**和**跟踪文件**关键字的详细信息，请参阅[ODBC 子键](../../../odbc/reference/install/odbc-subkey.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|创建数据源|[SQLCreate数据源](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|
