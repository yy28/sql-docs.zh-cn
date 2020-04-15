---
title: SQL创建数据源函数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCreateDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCreateDataSource
helpviewer_keywords:
- SQLCreateDataSource function [ODBC]
ms.assetid: 76ee851a-dca9-40cc-8e9e-eb3f74e560ee
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94dc0d6d6f3b5bc96ae41aecda5b46f119cff85c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301197"
---
# <a name="sqlcreatedatasource-function"></a>SQLCreateDataSource 函数
**一致性**  
 版本介绍： ODBC 2.0  
  
 **摘要**  
 **SQLCreateDataSource**显示一个对话框，用户可以使用该对话框添加数据源。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLCreateDataSource(  
     HWND    hwnd,  
     LPSTR   lpszDS);  
```  
  
## <a name="arguments"></a>参数  
 *霍恩德*  
 [输入]父窗口句柄。  
  
 *lpszDS*  
 [输入]数据源名称。 *lpszDS*可以是空指针或空字符串。  
  
## <a name="returns"></a>返回  
 如果创建了数据源 **，SQLCreateDataSource**将返回 TRUE。 否则，它将返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLCreateDataSource**返回 FALSE 时，可以通过调用**SQL 安装程序获取**关联的*\*pfError 代码*值。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|发生没有特定安装程序错误的错误。|  
|ODBC_ERROR_INVALID_HWND|无效的窗口句柄|*hwnd*参数无效或 NULL。|  
|ODBC_ERROR_INVALID_DSN|无效的 DSN|*lpszDS*参数包含一个对 DSN 无效的字符串。|  
|ODBC_ERROR_REQUEST_FAILED|*请求*失败|使用ODBC_ADD_DSN选项对**ConfigDSN**的调用失败。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|无法加载驱动程序或转换器设置库|无法加载驱动程序设置库。|  
|ODBC_ERROR_USER_CANCELED|用户取消的操作|用户取消了创建新数据源。|  
|ODBC_ERROR_CREATE_DSN_FAILED|无法创建请求的 DSN|无法连接到数据库;对**SQLDriverConnect**的文件 DSN 的调用未返回成功的连接。<br /><br /> 无法写入文件。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该功能。|  
  
## <a name="comments"></a>注释  
 如果*hwnd*为空 **，SQLCreate 数据源**将返回 FALSE。 否则，它将显示 **"创建新数据源**"对话框，其中包含用于选择要设置的数据源类型的向导页，如下图所示。  
  
 ![“创建新数据源”对话框：选择类型](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 默认选项是**文件数据源**。 选择数据源并单击**Next**后，将显示以下包含已安装驱动程序列表的向导页。  
  
 ![“创建新数据源”对话框：选择驱动程序](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 如果单击 **"取消"，** 对话框将消失 **，SQLCreateDataSource**将 FALSE 返回，错误代码为 ODBC_ERROR_USER_CANCELED。 如果选择了 **"用户数据源**"或 **"系统数据源"** 选项，则 **"高级**"按钮不可用。  
  
 单击"**下一步**"按钮时，将发生以下情况之一，具体取决于选择了哪种类型的数据源：  
  
-   如果选择了**文件数据源**，则将显示一个向导页，供用户输入文件名。  
  
-   如果选择了 **"用户数据源**"或 **"系统数据源**"，将显示显示数据源类型和驱动程序的向导页进行审阅，单击 **"完成"** 时，将设置数据源。  
  
 如果从"创建新数据源"向导页单击 **"高级"，** 则将显示一个向导页，供用户输入特定于驱动程序的信息。 在此对话框的文本框中，键入驱动程序和关键字以返回分隔，如下图所示。  
  
 ![“高级文件 DSN 创建设置”对话框](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 其他特定于驱动程序的关键字可以在**SQLDriverConnect**的描述中找到。 除**DSN**外，所有内容均允许。  
  
 **"验证此连接**"选项的默认值为 TRUE。 无论是否激活此向导页，此默认值都适用。 如果单击 **"确定"，** 则缓存文本框中指定的字符串和 **"验证此连接"** 选项值。 （如果单击"**关闭**"按钮或 **"取消"，** 则新输入的任何特定于驱动程序的信息都会丢失，因为文本框中指定的字符串和 **"验证此连接"** 选项值不会缓存。  
  
 如果在第一个向导页中选择了**文件数据源**，则在选择驱动程序并在高级向导页中输入关键字值后，系统将提示用户输入文件名。 单击 **"浏览"** 以搜索文件名，在这种情况下，"**浏览"** 框中的默认目录由 HKEY_LOCAL_MACHINE_SOFTWARE_Microsoft_Microsoft_Windows_CurrentVersion 和"ODBC_数据源"中的常见文件Dir指定的路径组合指定。 （如果 CommonFileDir 是"C：*程序文件\公共文件"，则默认目录为"C：程序文件\常见文件\ODBC_数据源"。  
  
 输入文件名并单击**Next**后，将对照操作系统的标准文件命名规则检查输入的文件名的有效性。 如果文件名无效，则错误消息框会通知用户已输入无效的文件名。 用户确认消息框后，焦点将返回到输入文件名的向导页。 如果文件名有效，将显示显示所选关键字值对的向导页供审阅，如下图所示。  
  
 ![“创建新数据源”对话框：检查](../../../odbc/reference/syntax/media/ch23d.gif "CH23D")  
  
 如果单击 **"完成"** 并选择**文件数据源**作为数据源类型，并且 **"验证此连接**选项为 TRUE"，则使用 **"保存文件"** 和 **"驱动程序"** 关键字调用**SQLDriverConnect。** *驱动程序完成*参数设置为SQL_DRIVER_COMPLETE。 **SAVEFILE**关键字的文件名是输入或选择的名称 **，DRIVER**关键字的驱动程序名称是所选的名称。 如果在高级向导页中指定了特定于驱动程序的连接字符串，则该字符串将追加到**DRIVER**关键字之后。  
  
 如果**SQLDriverConnect**返回SQL_SUCCESS，驱动程序管理器已创建文件 DSN。 **SQLCreate数据源**返回 TRUE。 如果**SQLDriverConnect**未返回SQL_SUCCESS，则警告消息框指示无法与数据源建立连接。 仍可创建具有最少连接信息的 DSN。 此消息框允许用户取消或继续创建文件 DSN。  
  
 如果用户选择继续创建 DSN，此过程将继续，就像**验证此连接**选项设置为 FALSE 一样。 如果用户选择取消，则为**SQLCreateDataSource**返回 FALSE，错误代码为ODBC_ERROR_CREATE_DSN_FAILED。  
  
 如果选择**文件数据源**作为数据源类型，并且 **"验证此连接**"选项为 FALSE，则使用**DRIVER**关键字创建文件 DSN，并从高级向导页创建用户指定的连接字符串（如果有）。 如果文件创建成功，则返回 TRUE 以用于**SQLCreateDataSource**。 如果文件创建不成功，则错误消息框会通知用户从操作系统返回的任何错误。 为**SQLCreateDataSource**返回 FALSE，错误代码为ODBC_ERROR_CREATE_DSN_FAILED。 有关文件数据源的详细信息，请参阅[使用文件数据源进行连接](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)，或请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 如果选择**用户**或**系统数据源**作为数据源类型，则使用 ODBC_ADD_DSN *fRequest*调用驱动程序设置库中的**ConfigDSN。** 有关详细信息，请参阅[配置DSN](../../../odbc/reference/syntax/configdsn-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|管理数据源|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
