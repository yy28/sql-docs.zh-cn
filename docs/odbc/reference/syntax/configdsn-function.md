---
title: 配置DSN功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- ConfigDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigDSN
helpviewer_keywords:
- ConfigDSN [ODBC]
ms.assetid: 01ced74e-c575-4a25-83f5-bd7d918123f8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fbae126c819088bd277621b207454503a86c8955
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306038"
---
# <a name="configdsn-function"></a>ConfigDSN 函数
**一致性**  
 版本介绍： ODBC 1.0  
  
 **摘要**  
 **配置DSN**添加、修改或删除系统信息中的数据源。 它可能会提示用户提供连接信息。 它可以在驱动程序 DLL 或单独的设置 DLL 中。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL ConfigDSN(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>参数  
 *hwnd 家长*  
 [输入]父窗口句柄。 如果句柄为空，则函数将不会显示任何对话框。  
  
 *f请求*  
 [输入]请求的类型。 *fRequest*参数必须包含以下值之一：  
  
 ODBC_ADD_DSN：添加新数据源。  
  
 ODBC_CONFIG_DSN：配置（修改）现有数据源。  
  
 ODBC_REMOVE_DSN：删除现有数据源。  
  
 *lpszDriver*  
 [输入]向用户而不是物理驱动程序名称显示的驱动程序描述（通常是关联的 DBMS 的名称）。  
  
 *lpsz属性*  
 [输入]以关键字-值对形式加倍终止的属性列表。 有关详细信息，请参阅"注释"。  
  
## <a name="returns"></a>返回  
 如果成功，则函数返回 TRUE，如果失败，则返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**ConfigDSN**返回 FALSE 时，通过调用**SQLPost 安装程序错误**将关联的*\*pfError 代码*值发布到安装程序错误缓冲区，并且可以通过调用**SQL 安装程序错误**获得。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|无效的窗口句柄|*hwnd 父参数*无效。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|无效关键字-值对|*lpszAttributes*参数包含语法错误。|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或翻译者姓名|*lpszDriver*参数无效。 在注册表中找不到它。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|无效的请求类型|*fRequest*参数不是以下参数之一：<br /><br /> ODBC_ADD_DSNODBC_CONFIG_DSNODBC_REMOVE_DSN|  
|ODBC_ERROR_REQUEST_FAILED|*请求*失败|无法执行*fRequest*参数请求的操作。|  
|ODBC_ERROR_DRIVER_SPECIFIC|驱动程序或转换器特定错误|驱动程序特定的错误，没有定义的 ODBC 安装程序错误。 调用**SQLPost 安装程序错误**函数时 *，SzError*参数应包含特定于驱动程序的错误消息。|  
  
## <a name="comments"></a>注释  
 **ConfigDSN**从安装程序 DLL 接收连接信息，作为关键字-值对形式的属性列表。 每个对都用空字节终止，整个列表用空字节终止。 （即，两个空字节标记列表的末尾。关键字值对中的等号周围不允许空格。 **配置DSN**可以接受不是**SQLBrowseConnect**和**SQLDriverConnect**的有效关键字。 **配置DSN**不一定支持所有关键字，是有效的关键字**的SQLBrowse连接**和**SQLDriver连接**。 （**配置DSN**不接受**DRIVER**关键字。**ConfigDSN**函数使用的关键字必须支持使用安装程序的 AUTO 设置功能重新创建数据源所需的所有选项。 当**ConfigDSN**值和连接字符串值的使用相同时，应使用相同的关键字。  
  
 与**SQLBrowseConnect**和**SQLDriverConnect**中一样，关键字及其值不应包含 ***（"";？？{}\**！]** 字符和**DSN**关键字的值不能仅包含空白。 由于注册表语法，关键字和数据源名称不能包含反斜杠 （\\） 字符。  
  
 **ConfigDSN**应调用**SQLValidDSN**来检查数据源名称的长度，并验证名称中是否不包含无效字符。 如果数据源名称长于SQL_MAX_DSN_LENGTH或包含无效字符 **，SQLValidDSN**将返回错误 **，ConfigDSN**将返回错误。 **SQLWriteDSNToIni**也检查数据源名称的长度。  
  
 例如，要配置需要用户 ID、密码和数据库名称的数据源，安装程序可能会传递以下关键字-值对：  
  
```  
DSN=Personnel Data\0UID=Smith\0PWD=Sesame\0DATABASE=Personnel\0\0  
```  
  
 有关这些关键字的详细信息，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)和每个驱动程序的文档。  
  
 要显示对话框 *，hwndParent*不能为空。  
  
## <a name="adding-a-data-source"></a>添加数据源  
 如果数据源名称在*lpszAttributes*中传递到**ConfigDSN，****则 ConfigDSN**将检查该名称是否有效。 如果数据源名称与现有数据源名称匹配，并且*hwndParent*为 null，**则 ConfigDSN**将覆盖现有名称。 如果它与现有名称匹配，并且*hwndParent*不为空 **，ConfigDSN**会提示用户覆盖现有名称。  
  
 如果*lpszAttributes*包含足够的信息以连接到数据源 **，ConfigDSN**可以添加数据源或显示一个对话框，用户可以使用该对话框更改连接信息。 如果 lpszAttributes 不包含足够的信息以连接到数据源，ConfigDSN 必须确定必要的信息;如果*lpszAttributes*没有包含足够的信息来连接到数据源。因此 **，ConfigDSN**必须确定必要的信息。如果*hwndParent*不为空，则显示一个对话框，用于从用户中检索信息。  
  
 如果**ConfigDSN**显示一个对话框，它必须在*lpszAttributes*中显示传递给它的任何连接信息。 特别是，如果数据源名称传递给它 **，ConfigDSN**将显示该名称，但不允许用户更改该名称。 **ConfigDSN**可以为未在*lpszAttributes*中传递给它的连接信息提供默认值。  
  
 如果**ConfigDSN**无法获取数据源的完整连接信息，它将返回 FALSE。  
  
 如果**ConfigDSN**可以获取数据源的完整连接信息，它将在安装程序 DLL 中调用**SQLWriteDSNToini**以将新的数据源规范添加到 Odbc.ini 文件（或注册表）。 **SQLWriteDSNToI**将数据源名称添加到 [ODBC 数据源] 部分，创建数据源规范部分，并将**DRIVER**关键字与驱动程序描述作为其值。 **配置DSN**在安装程序 DLL 中调用**SQLWritePrivateProfileString**来添加驱动程序使用的任何其他关键字和值。  
  
## <a name="modifying-a-data-source"></a>修改数据源  
 要修改数据源，必须在*lpszAttributes*中将数据源名称传递给**ConfigDSN。** **配置DSN**检查数据源名称是否位于 Odbc.ini 文件（或注册表）中。  
  
 如果*hwndParent*为空 **，ConfigDSN**将使用*lpszAttributes*中的信息来修改 Odbc.ini 文件（或注册表）中的信息。 如果*hwndParent*不是 null，**则 ConfigDSN**将显示一个对话框，使用*lpszAttributes*中的信息;对于不在*lpszAttributes*中的信息，它使用来自系统信息的信息。 用户可以在**ConfigDSN**将其存储在系统信息之前对其进行修改。  
  
 如果数据源名称已更改 **，ConfigDSN**首先在安装程序 DLL 中调用**SQLRemoveDSNFromIni，** 以从 Odbc.ini 文件（或注册表）中删除现有的数据源规范。 然后，按照上一节中的步骤添加新的数据源规范。 如果未更改数据源名称 **，ConfigDSN**在安装程序 DLL 中调用**SQLWritePrivateProfileString**进行任何其他更改。 **配置DSN**不得删除或更改**驱动程序**关键字的值。  
  
## <a name="deleting-a-data-source"></a>删除数据源  
 要删除数据源，必须在*lpszAttributes*中将数据源名称传递给**ConfigDSN。** **配置DSN**检查数据源名称是否位于 Odbc.ini 文件（或注册表）中。 然后，它会在安装程序 DLL 中调用**SQLRemoveDSNFromini**以删除数据源。  
  
## <a name="note"></a>注意
 如果编写此例程的 Unicode 版本，则必须将其称为**ConfigDSNW，** 使用 LPCWSTR 参数而不是 LPCSTR。
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|添加、修改或删除数据源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|从 Odbc.ini 文件或注册表获取值|[SQLGet 私人配置文件字符串](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|  
|删除默认数据源|[SQL 删除默认数据源](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|从 Odbc.ini（或注册表）中删除数据源名称|[SQLRemoveDSNfromini](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|将数据源名称添加到 Odbc.ini（或注册表）|[SQLwriteSntoini](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|  
|将值写入 Odbc.ini 文件或注册表|[SQLWrite 私有配置文件字符串](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
