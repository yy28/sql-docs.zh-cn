---
title: ConfigDSN 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d65b7f31010aeb768f7b04c06753f185d3cc792f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232038"
---
# <a name="configdsn-function"></a>ConfigDSN 函数
**符合性**  
 版本引入了：ODBC 1.0  
  
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
 [输入]父窗口句柄。 如果句柄为空，该函数将不显示任何对话框。  
  
 *fRequest*  
 [输入]请求的类型。 *FRequest*参数必须包含以下值之一：  
  
 ODBC_ADD_DSN:添加新的数据源。  
  
 ODBC_CONFIG_DSN:配置 （修改） 的现有数据源。  
  
 ODBC_REMOVE_DSN:删除现有数据源。  
  
 *lpszDriver*  
 [输入]驱动程序说明 （通常关联 DBMS 的名称） 提供给用户而不是物理驱动器的名称。  
  
 *lpszAttributes*  
 [输入]双向以 null 结尾的关键字 / 值对的窗体中的属性列表。 有关详细信息，请参阅"注释"。  
  
## <a name="returns"></a>返回  
 如果成功，则返回 FALSE 出现故障时，该函数返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**ConfigDSN**返回 FALSE，关联 *\*pfErrorCode*值通过调用传递到安装程序错误缓冲区**SQLPostInstallerError**和可以通过调用来获取**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|窗口句柄无效|*HwndParent*参数无效。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|无效的关键字值对|*LpszAttributes*参数包含语法错误。|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或转换器名称|*LpszDriver*参数无效。 它找不到注册表中。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|请求的类型无效|*FRequest*参数不是以下之一：<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN|  
|ODBC_ERROR_REQUEST_FAILED|*请求*失败|无法执行请求的操作*fRequest*参数。|  
|ODBC_ERROR_DRIVER_SPECIFIC|特定于驱动程序或转换器错误|没有任何定义的 ODBC 安装程序错误特定于驱动程序的错误。 *SzError*调用中的参数**SQLPostInstallerError**函数应包含特定于驱动程序的错误消息。|  
  
## <a name="comments"></a>注释  
 **ConfigDSN**收到连接信息从安装程序 DLL 作为中的关键字值对形式的属性列表。 每个对终止 null 字节，并且整个列表终止 null 字节。 （也就是说，两个 null 字节标记列表的末尾。）关键字值对中的等号两侧不允许有空格。 **ConfigDSN**可以接受不是有效的关键字的关键字**SQLBrowseConnect**并**SQLDriverConnect**。 **ConfigDSN**不会不一定支持所有关键字都是有效的关键字**SQLBrowseConnect**并**SQLDriverConnect**。 (**ConfigDSN**不接受**驱动程序**关键字。)使用的关键字**ConfigDSN**函数必须支持重新创建数据源使用自动安装功能的安装程序所需的所有选项。 时的用法**ConfigDSN**值和连接字符串值是相同的应使用相同的关键字。  
  
 在中作为**SQLBrowseConnect**并**SQLDriverConnect**，关键字和它们的值不应包含 **[]{}（)，;？\*= ！ @** 个字符和的值**DSN**关键字不能只包含空格。 由于注册表语法，关键字和数据源名称不能包含反斜杠 (\\) 字符。  
  
 **ConfigDSN**应调用**SQLValidDSN**以检查数据源名称的长度并确保在名称中包含任何无效字符。 如果数据源名称的长度超过 SQL_MAX_DSN_LENGTH 或包含无效字符**SQLValidDSN**将返回错误并**ConfigDSN**返回错误。 此外通过检查数据源名称的长度**SQLWriteDSNToIni**。  
  
 例如，若要配置需要用户 ID、 密码和数据库名称的数据源，请安装应用程序可能会传递以下关键字值对：  
  
```  
DSN=Personnel Data\0UID=Smith\0PWD=Sesame\0DATABASE=Personnel\0\0  
```  
  
 有关这些关键字的详细信息，请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)和每个驱动程序的文档。  
  
 若要显示的对话框*hwndParent*不能为 null。  
  
## <a name="adding-a-data-source"></a>添加数据源  
 如果数据源名称传递给**ConfigDSN**中*lpszAttributes*， **ConfigDSN**检查该名称是否有效。 如果数据源名称与现有数据源名称相匹配并*hwndParent*为 null， **ConfigDSN**将覆盖现有的名称。 如果它匹配现有的名称和*hwndParent*不为 null， **ConfigDSN**会提示用户覆盖现有的名称。  
  
 如果*lpszAttributes*包含足够的信息来连接到数据源**ConfigDSN**可以添加数据源，或显示与该用户可以更改连接信息的对话框。 如果*lpszAttributes*不包含足够的信息来连接到数据源**ConfigDSN**必须确定所需的信息; 如果*hwndParent*不为 null，它将显示一个对话框，从用户检索信息。  
  
 如果**ConfigDSN**显示一个对话框，它必须显示中传递给它的任何连接信息*lpszAttributes*。 具体而言，数据源名称传递给它，如果**ConfigDSN**显示该名称，但不允许用户对其进行更改。 **ConfigDSN**可以提供连接信息不会传递给它的默认值*lpszAttributes*。  
  
 如果**ConfigDSN**无法获取完整的连接信息对于数据源，它将返回 FALSE。  
  
 如果**ConfigDSN**可以获取数据源的完整的连接信息，它将调用**SQLWriteDSNToIni**安装程序 DLL 将新数据源说明添加到 Odbc.ini 文件 （或注册表） 中。 **SQLWriteDSNToIni**将数据源名称添加到 [ODBC 数据源] 节，创建数据源规范部分，并将**驱动程序**关键字与驱动程序作为其值的描述。 **ConfigDSN**调用**SQLWritePrivateProfileString**在安装程序 DLL，若要添加的任何其他关键字和驱动程序使用的值。  
  
## <a name="modifying-a-data-source"></a>修改数据源  
 若要修改的数据源，必须将数据源名称传递给**ConfigDSN**中*lpszAttributes*。 **ConfigDSN**会检查是否在 Odbc.ini 文件 （或注册表） 中的数据源名称。  
  
 如果*hwndParent*为 null， **ConfigDSN**使用中的信息*lpszAttributes*修改 Odbc.ini 文件 （或注册表） 中的信息。 如果*hwndParent*不为 null， **ConfigDSN**显示使用中的信息的对话框*lpszAttributes*; 有关信息不在*lpszAttributes*，它将使用从系统信息的信息。 用户可以修改信息，然后**ConfigDSN**将其存储在系统信息。  
  
 如果更改数据源名称，请**ConfigDSN**首先调用**SQLRemoveDSNFromIni**在安装程序 DLL，若要删除的现有数据源从 Odbc.ini 文件 （或注册表） 的规范。 然后，它按照要添加新数据源说明的前面部分中的步骤。 如果未更改的数据源名称， **ConfigDSN**调用**SQLWritePrivateProfileString**在安装程序 DLL 要进行任何其他更改。 **ConfigDSN**可能会删除或更改的值**驱动程序**关键字。  
  
## <a name="deleting-a-data-source"></a>删除数据源  
 若要删除的数据源，必须将数据源名称传递给**ConfigDSN**中*lpszAttributes*。 **ConfigDSN**会检查是否在 Odbc.ini 文件 （或注册表） 中的数据源名称。 然后，它调用**SQLRemoveDSNFromIni**安装程序 DLL，若要删除数据源中。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|添加、 修改或删除数据源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|获取从 Odbc.ini 文件或注册表值|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|  
|删除默认数据源|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|从 Odbc.ini （或注册表） 中删除数据源名称|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|将数据源名称添加到 Odbc.ini （或注册表）|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|  
|写入 Odbc.ini 文件或注册表值|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
