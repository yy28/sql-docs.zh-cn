---
title: ConfigDSN 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7a8b75fb1b87a4f6199999e5d5e33d8cd0083bac
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32920772"
---
# <a name="configdsn-function"></a>ConfigDSN 函数
**一致性**  
 版本引入了： ODBC 1.0  
  
 **摘要**  
 **ConfigDSN**添加、 修改或删除数据源中的系统信息。 它可能会提示用户输入连接信息。 它可以是驱动程序 DLL 或单独的安装程序 DLL。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL ConfigDSN(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>参数  
 *hwndParent*  
 [输入]父窗口句柄。 如果句柄为 null，函数将不显示任何对话框。  
  
 *fRequest*  
 [输入]请求的类型。 *FRequest*参数必须包含以下值之一：  
  
 ODBC_ADD_DSN： 添加新的数据源。  
  
 ODBC_CONFIG_DSN： 配置 （修改） 的现有数据源。  
  
 ODBC_REMOVE_DSN： 删除现有数据源。  
  
 *lpszDriver*  
 [输入]驱动程序说明 （通常名称关联的 DBMS） 呈现给用户，而不是物理驱动器的名称。  
  
 *lpszAttributes*  
 [输入]双向以 null 结尾的关键字 / 值对窗体中的属性列表。 有关详细信息，请参阅"注释"。  
  
## <a name="returns"></a>返回  
 如果它成功，则返回 FALSE 如果失败，则函数将返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**ConfigDSN**返回 FALSE，一个关联 *\*pfErrorCode*值发布到安装程序错误缓冲区调用**SQLPostInstallerError**和可以通过调用获取**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError**并解释此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|窗口句柄无效|*HwndParent*自变量无效。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|无效的关键字 / 值对|*LpszAttributes*参数包含语法错误。|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或转换器名称|*LpszDriver*自变量无效。 它找不到注册表中。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|请求的类型无效|*FRequest*自变量不是以下之一：<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN|  
|ODBC_ERROR_REQUEST_FAILED|*请求*失败|无法执行请求的操作*fRequest*自变量。|  
|ODBC_ERROR_DRIVER_SPECIFIC|特定于驱动程序或转换器错误|没有任何定义的 ODBC 安装程序错误特定于驱动程序的错误。 *SzError*对的调用中的自变量**SQLPostInstallerError**函数应包含特定于驱动程序的错误消息。|  
  
## <a name="comments"></a>注释  
 **ConfigDSN**的关键字 / 值对形式的属性列表作为安装程序 DLL 的接收连接信息。 每个对终止与 null 字节，并且整个列表因 null 字节。 （也就是说，两个 null 字节标记列表的末尾。）中的关键字 / 值对的等号两侧不允许有空格。 **ConfigDSN**可以接受不是有效的关键字的关键字**SQLBrowseConnect**和**SQLDriverConnect**。 **ConfigDSN**不一定支持所有关键字都是有效的关键字**SQLBrowseConnect**和**SQLDriverConnect**。 (**ConfigDSN**不接受**驱动程序**关键字。)使用的关键字**ConfigDSN**函数必须支持重新创建数据源使用的安装程序自动安装程序功能所需的所有选项。 时的用法的**ConfigDSN**值和连接字符串值相同，应使用相同的关键字。  
  
 作为 in **SQLBrowseConnect**和**SQLDriverConnect**，关键字和它们的值不应包含 **[]{}（)，;？\*= ！ @** 字符和的值**DSN**关键字不能只包含空白。 由于注册表语法中，关键字和数据源名称不能包含反斜杠 (\\) 字符。  
  
 **ConfigDSN**应调用**SQLValidDSN**检查数据源名称的长度并确认在名称中包含任何无效字符。 如果数据源名称的长度超过 SQL_MAX_DSN_LENGTH 或包含无效字符， **SQLValidDSN**返回错误和**ConfigDSN**返回错误。 通过检查程序数据源名称的长度**SQLWriteDSNToIni**。  
  
 例如，若要配置的数据源，需要用户 ID、 密码和数据库名称，安装应用程序可能会传递以下关键字 / 值对：  
  
```  
DSN=Personnel Data\0UID=Smith\0PWD=Sesame\0DATABASE=Personnel\0\0  
```  
  
 有关这些关键字的详细信息，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)和每个驱动程序的文档。  
  
 若要显示一个对话框， *hwndParent*不得为空。  
  
## <a name="adding-a-data-source"></a>添加数据源  
 如果数据源名称传递给**ConfigDSN**中*lpszAttributes*， **ConfigDSN**检查该名称是否有效。 如果数据源名称与现有的数据源名称相匹配和*hwndParent*为 null， **ConfigDSN**将覆盖现有名称。 如果它与现有的名称相匹配和*hwndParent*不为 null， **ConfigDSN**会提示用户进行覆盖现有名称。  
  
 如果*lpszAttributes*包含足够的信息来连接到数据源， **ConfigDSN**可以添加数据源，或者显示一个对话框，用户可以与其更改连接信息。 如果*lpszAttributes*不包含足够的信息来连接到数据源， **ConfigDSN**必须确定所需的信息; 如果*hwndParent*不为 null，它显示一个对话框，从用户检索信息。  
  
 如果**ConfigDSN**显示一个对话框，它必须显示中传递给它的任何连接信息*lpszAttributes*。 具体而言，如果数据源名称已传递给它， **ConfigDSN**显示该名称，但不允许用户更改它。 **ConfigDSN**可以提供连接信息不传递给它的默认值*lpszAttributes*。  
  
 如果**ConfigDSN**无法获取完整的连接信息对于数据源，它将返回 FALSE。  
  
 如果**ConfigDSN**可以获取数据源的完整的连接信息时，它调用**SQLWriteDSNToIni**在安装程序中向 Odbc.ini 文件 （或注册表） 中添加新的数据源说明的 DLL。 **SQLWriteDSNToIni**将数据源名称添加到 [ODBC 数据源] 节、 创建数据源规范节，并添加**驱动程序**关键字作为其值的驱动程序说明。 **ConfigDSN**调用**SQLWritePrivateProfileString**在安装程序 DLL 以添加任何其他关键字和驱动程序所使用的值。  
  
## <a name="modifying-a-data-source"></a>修改数据源  
 若要修改的数据源，必须将数据源名称传递给**ConfigDSN**中*lpszAttributes*。 **ConfigDSN**的数据源名称所采用的 Odbc.ini 文件 （或注册表） 的检查。  
  
 如果*hwndParent*为 null， **ConfigDSN**使用中的信息*lpszAttributes*修改 Odbc.ini 文件 （或注册表） 中的信息。 如果*hwndParent*不为 null， **ConfigDSN**显示一个对话框，使用中的信息*lpszAttributes*; 有关信息不在*lpszAttributes*，它将使用从系统信息的信息。 用户可以修改信息，然后**ConfigDSN**将其存储在系统信息。  
  
 如果数据源名称已更改， **ConfigDSN**首先调用**SQLRemoveDSNFromIni**在安装程序 DLL，若要删除的现有数据源从 Odbc.ini 文件 （或注册表） 的规范。 然后，它将按照在上一部分中添加新的数据源说明的步骤。 如果未更改的数据源名称， **ConfigDSN**调用**SQLWritePrivateProfileString**在安装程序中进行任何其他更改的 DLL。 **ConfigDSN**可能不删除或更改的值**驱动程序**关键字。  
  
## <a name="deleting-a-data-source"></a>删除数据源  
 若要删除数据源，必须将数据源名称传递给**ConfigDSN**中*lpszAttributes*。 **ConfigDSN**的数据源名称所采用的 Odbc.ini 文件 （或注册表） 的检查。 然后，它调用**SQLRemoveDSNFromIni**在安装程序中删除数据源的 DLL。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|添加、 修改或删除数据源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|从 Odbc.ini 文件或注册表中获取一个值|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|  
|删除默认数据源|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|从 Odbc.ini （或注册表） 中删除数据源名称|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|将数据源名称添加到 Odbc.ini （或注册表）|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|  
|写入的 Odbc.ini 文件或注册表值|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
