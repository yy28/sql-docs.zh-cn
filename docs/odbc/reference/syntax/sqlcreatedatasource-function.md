---
title: SQLCreateDataSource 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5e06c511debbcac9741e178ebfb5c1a8eae0a330
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47620405"
---
# <a name="sqlcreatedatasource-function"></a>SQLCreateDataSource 函数
**符合性**  
 版本引入了： ODBC 2.0  
  
 **摘要**  
 **SQLCreateDataSource**显示一个对话框，用户可以使用该对话框添加数据源。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL SQLCreateDataSource(  
     HWND    hwnd,  
     LPSTR   lpszDS);  
```  
  
## <a name="arguments"></a>参数  
 *hwnd*  
 [输入]父窗口句柄。  
  
 *lpszDS*  
 [输入]数据源名称。 *lpszDS*可以是 null 指针或空字符串。  
  
## <a name="returns"></a>返回  
 **SQLCreateDataSource**如果创建数据源，则返回 TRUE。 否则，它返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLCreateDataSource**返回 FALSE，关联 *\*pfErrorCode*可以通过调用获取的值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|出错的其中没有特定的安装程序错误。|  
|ODBC_ERROR_INVALID_HWND|窗口句柄无效|*Hwnd*参数为无效或为 NULL。|  
|ODBC_ERROR_INVALID_DSN|无效的 DSN|*LpszDS*参数包含无效的 DSN 的字符串。|  
|ODBC_ERROR_REQUEST_FAILED|*请求*失败|在调用**ConfigDSN** ODBC_ADD_DSN 选项失败。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|无法加载驱动程序或转换器安装程序库|无法加载驱动程序安装程序库。|  
|ODBC_ERROR_USER_CANCELED|用户已取消操作|用户已取消创建新的数据源。|  
|ODBC_ERROR_CREATE_DSN_FAILED|无法创建请求的 DSN|无法连接到该数据库。在调用**SQLDriverConnect**为文件 DSN 未返回成功的连接。<br /><br /> 无法写入到文件。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 如果*hwnd*为 null， **SQLCreateDataSource**返回 FALSE。 否则，将显示**创建新的数据源**与向导页用于选择要进行设置、 数据源的类型，如以下插图所示的对话框。  
  
 ![创建新的数据源对话框中： 选择类型](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 默认选项是**文件数据源**。 当数据源已被选并**下一步**单击，将显示以下向导页面，其中包含安装的驱动程序的列表。  
  
 ![创建新的数据源对话框中： 选择驱动程序](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 如果**取消**单击时，对话框框将立即消失并**SQLCreateDataSource** ODBC_ERROR_USER_CANCELED 的错误代码，则返回 FALSE。 如果任一**用户数据源**或**系统数据源**选择了选项，**高级**按钮将不可用。  
  
 当**下一步**单击按钮时，将发生下列情况之一，具体取决于哪种类型的数据选择源：  
  
-   如果**文件数据源**已选中，向导页会显示用户无法输入文件名称。  
  
-   如果任一**用户数据源**或**系统数据源**已选中，向导显示的数据源和驱动程序的类型会显示一个页面进行审阅，以及何时**完成**是单击，数据源设置。  
  
 如果**高级**单击创建新的数据源向导页上，从向导页上显示用户无法输入特定于驱动程序的信息。 在此对话框中的文本框中，键入以下插图所示的驱动程序和关键字，以回车符分隔。  
  
 ![高级文件 DSN 创建设置对话框](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 描述下找不到其他特定于驱动程序的关键字**SQLDriverConnect**。 除之外的所有**DSN**允许。  
  
 默认值为**验证此连接**选项是 TRUE。 无论激活此向导页，将应用此默认值。 如果**确定**单击时，在文本框中指定的字符串并**验证此连接**缓存选项值。 (如果**关闭**按钮或**取消**单击时，任何新输入特定于驱动程序的信息会丢失，因为在文本框中指定的字符串和**验证此连接**不会被缓存选项值。)  
  
 如果**文件数据源**中第一个向导页上，已选择，则已选择驱动程序，并且已在高级的向导页中输入关键字值后，提示用户输入文件名称。 单击**浏览**要搜索的文件名称，在这种情况下中的默认目录**浏览**CommonFileDir HKEY_LOCAL_MACHINE\SOFTWARE\ 中指定的路径的组合来指定框Microsoft\Windows\CurrentVersion 和"ODBC\DataSources"。 （如果 CommonFileDir 为"C:\Program Files\Common Files"，默认目录将是"C:\Program Files\Common Files\ODBC\Data 源"。）  
  
 当已输入文件名称和**下一步**单击时，该文件根据标准的操作系统文件命名规则的有效性检查输入的名称。 如果文件名无效，错误消息框会通知用户输入了无效的文件名称。 用户确认消息框后，焦点将返回到向导页中输入的文件的名称。 如果文件名称是否有效，一个显示所选的关键字 / 值对的向导页面显示供审核下, 图中所示。  
  
 ![创建新的数据源对话框中： 查看](../../../odbc/reference/syntax/media/ch23d.gif "CH23D")  
  
 如果**完成**单击和**文件数据源**选为数据源类型，并且如果**验证此连接**选项是 TRUE， **SQLDriverConnect**使用调用**SAVEFILE**并**驱动程序**关键字。 *DriverCompletion*参数设置为 SQL_DRIVER_COMPLETE。 文件名**SAVEFILE**关键字是已输入的名称或所选和驱动程序名称**驱动程序**关键字是选择的名称。 如果在高级的向导页中指定了特定于驱动程序的连接字符串，该字符串将追加后**驱动程序**关键字。  
  
 如果**SQLDriverConnect**返回 SQL_SUCCESS，驱动程序管理器已创建文件 DSN。 **SQLCreateDataSource** ，则返回 TRUE。 如果**SQLDriverConnect**不会返回 SQL_SUCCESS，一条警告消息框指示无法与数据源建立连接。 仍可创建使用最少的连接信息的 DSN。 此消息框，用户可以使用取消或继续执行文件 DSN 创建。  
  
 如果用户选择继续创建 DSN，此过程将继续像**验证此连接**选项已设置为 FALSE。 如果用户选择取消，则为返回 FALSE **SQLCreateDataSource**并 ODBC_ERROR_CREATE_DSN_FAILED 返回错误代码。  
  
 如果**文件数据源**选为数据源类型和**验证此连接**选项为 FALSE，使用创建文件 DSN**驱动程序**关键字和用户指定高级的向导页从连接字符串 （如果有）。 如果文件创建成功，则为返回 TRUE **SQLCreateDataSource**。 如果文件创建未成功完成，错误消息框将通知从操作系统返回任何错误的用户。 对于返回 FALSE **SQLCreateDataSource**并 ODBC_ERROR_CREATE_DSN_FAILED 返回错误代码。 有关文件的数据源的详细信息，请参阅[连接使用的文件数据源](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)，或请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 如果**用户**或**系统数据源**作为数据源类型，选择**ConfigDSN**驱动程序安装程序中使用 ODBC_ADD_DSN 调用库*fRequest*。 有关详细信息，请参阅[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|管理数据源|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
