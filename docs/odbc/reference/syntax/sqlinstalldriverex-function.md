---
title: SQLInstallDriverEx 功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallDriverEx
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallDriverEx
helpviewer_keywords:
- SQLInstallDriverEx function [ODBC]
ms.assetid: 1dd74544-f4e9-46e1-9b5f-c11d84fdab4c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 054e8b6b9eae26bd5f973f3d46d7ef37363a8e79
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302119"
---
# <a name="sqlinstalldriverex-function"></a>SQLInstallDriverEx 函数
**一致性**  
 版本介绍： ODBC 3.0  
  
 **摘要**  
 **SQLInstallDriverEx**在系统信息中将有关驱动程序的信息添加到 Odbcinst.ini 条目，并将驱动程序的使用*计数*增加 1。 但是，如果驱动程序的版本已存在，但驱动程序的 *"使用情况计数"* 值不存在，则新的 *"使用计数"* 值设置为 2。  
  
 此函数实际上不会复制任何文件。 调用程序负责将驱动程序的文件正确复制到目标目录。  
  
 **SQLInstallDriverEx**的功能也可以与[ODBCCONF 一起访问。EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLInstallDriverEx(  
     LPCSTR    lpszDriver,  
     LPCSTR    lpszPathIn,  
     LPSTR     lpszPathOut,  
     WORD      cbPathOutMax,  
     WORD *    pcbPathOut,  
     WORD      fRequest,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>参数  
 *lpszDriver*  
 [输入]向用户而不是物理驱动程序名称显示的驱动程序描述（通常是关联的 DBMS 的名称）。 *lpszDriver*参数必须包含描述驱动程序的关键字值对的双 null 终止列表。 有关关键字-值对的详细信息，请参阅[驱动程序规范子键](../../../odbc/reference/install/driver-specification-subkeys.md)。 有关双空终止字符串的详细信息，请参阅[ConfigDSN 函数](../../../odbc/reference/syntax/configdsn-function.md)。  
  
 *lpszPathin*  
 [输入]安装的目标目录的完整路径或空指针。 如果*lpszPathIn*是空指针，则驱动程序将安装在系统目录中。  
  
 *lpszPathOut*  
 [输出]应安装驱动程序的目标目录的路径。 如果以前未安装驱动程序，*则 lpszPathOut*应与*lpszPathIn*相同。 如果以前安装了驱动程序，则*lpszPathOut*是上次安装的路径。  
  
 *cbPathOutMax*  
 [输入]*长度的lpszPathOut。*  
  
 *多巴帕路*  
 [输出]可用以*lpszPathOut*返回的字节总数（不包括空终止字符）。 如果可用于返回的字节数大于或等于*cbPathOutMax，**则 lpszPathOut*中的输出路径将截断为*cbPathOutMax*减去 null 终止字符。 *pcbPathOut*参数可以是空指针。  
  
 *f请求*  
 [输入]请求的类型。 *fRequest*参数必须包含以下值之一：  
  
 ODBC_INSTALL_INQUIRY：询问驱动程序的安装位置。  
  
 ODBC_INSTALL_COMPLETE：完成安装请求。  
  
 *lpdwUsageCount*  
 [输出]调用此函数后驱动程序的使用计数。  
  
 应用程序不应设置使用计数。 ODBC 将保留此计数。  
  
## <a name="returns"></a>返回  
 如果成功，则函数返回 TRUE，如果失败，则返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLInstallDriverEx**返回 FALSE 时，可以通过调用**SQL 安装程序错误**获得关联的*\*pfErrorCode*值。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|发生没有特定安装程序错误的错误。|  
|ODBC_ERROR_INVALID_BUFF_LEN|无效的缓冲区长度|*lpszPathOut*参数不够大，无法包含输出路径。 缓冲区包含截断路径。<br /><br /> *cbPathOutMax*参数为*0，fRequest*是ODBC_INSTALL_COMPLETE。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|无效的请求类型|*fRequest*参数不是以下参数之一：<br /><br /> ODBC_INSTALL_INQUIRYODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|无效关键字-值对|*lpszDriver*参数包含语法错误。|  
|ODBC_ERROR_INVALID_PATH|无效安装路径|*lpszPathIn*参数包含一个无效的路径。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|无法加载驱动程序或转换器设置库|无法加载驱动程序设置库。|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|无效参数序列|*lpszDriver*参数不包含关键字-值对的列表。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|无法增加或递减组件使用量计数|安装程序未能增加驱动程序的使用计数。|  
  
## <a name="comments"></a>注释  
 *lpszDriver*参数是关键字-值对形式的属性列表。 每个对都用空字节终止，整个列表用空字节终止。 （即，两个空字节标记列表的末尾。此列表的格式如下：  
  
 _驱动程序-desc_ **\\**0**=** 驱动程序 _-DLL 文件名_**\\****=** 0[_设置设置-DLL 文件名_<b>\\</b>0]  
  
 [_驱动程序-attr-关键字1_**=**_值1_<b>\\</b>0][_驱动程序-attr-关键字2_**=**_值2_<b>\\</b>0]...<b>\\</b>0  
  
 其中 \0 是空字节，*驱动程序 attr-关键字*是任何驱动程序属性关键字。 关键字必须按指定顺序显示。 例如，假设格式化文本文件的驱动程序具有单独的驱动程序并设置 DLL，并且可以使用具有 .txt 和 .csv 扩展名的文件。 此驱动程序的*lpszDriver*参数可能如下所示：  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 假设 SQL Server 的驱动程序没有单独的设置 DLL，并且没有任何驱动程序属性关键字。 此驱动程序的*lpszDriver*参数可能如下所示：  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 **SQLInstallDriverEx**从*lpszDriver*参数中检索有关驱动程序的信息后，它将驱动程序描述添加到系统信息中的 Odbcinst.ini 条目的 [ODBC 驱动程序] 部分。 然后，它创建一个标题为驱动程序说明的部分，并添加驱动程序 DLL 和设置 DLL 的完整路径。 最后，它返回安装的目标目录的路径，但不会将驱动程序文件复制到它。 调用程序必须实际将驱动程序文件复制到目标目录。  
  
 **SQLInstallDriverEx**将已安装驱动程序的组件使用量计数增加 1。 如果驱动程序的版本已存在，但驱动程序的组件使用计数不存在，则新的组件使用计数值设置为 2。  
  
 应用程序安装程序负责物理复制驱动程序文件和维护文件使用情况计数。 如果以前未安装驱动程序文件，应用程序安装程序必须在*lpszPathIn*路径中复制该文件并创建文件使用情况计数。 如果以前已安装该文件，安装程序只会增加文件使用情况计数，并在*lpszPathOut*参数中返回先前安装的路径。  
  
> [!NOTE]  
>  有关组件使用情况计数和文件使用情况计数的详细信息，请参阅[使用情况计数](../../../odbc/reference/install/usage-counting.md)。  
  
 如果应用程序以前安装了旧版本的驱动程序文件，则应卸载驱动程序，然后重新安装驱动程序，以便驱动程序组件使用计数有效。 应首先调用**SQLConfigDriver（** 带有 ODBC_REMOVE_DRIVER*请求*），然后调用**SQLRemoveDriver**以减少组件使用计数。 然后应调用**SQLInstallDriverEx**重新安装驱动程序，从而增加组件使用计数。 应用程序安装程序必须用新文件替换旧文件。 文件使用情况计数将保持不变，使用旧版本文件的任何其他应用程序现在都将使用较新版本。  
  
> [!NOTE]  
>  如果以前安装了驱动程序，并且调用**SQLInstallDriverEx**将驱动程序安装在其他目录中，则该功能将返回 TRUE，但*lpszPathOut*将包含已安装驱动程序的目录。 它将不包括在*lpszDriver*参数中输入的目录。  
  
 **SQLInstallDriverEx**中的*lpszPathOut*中的路径长度允许两阶段安装过程，因此应用程序可以通过使用 ODBC_INSTALL_INQUIRY 模式的*fRequest*调用**SQLInstallDriverEx**来确定应该是什么*cbPathOutMax。* 这将返回*pcbPathOut*缓冲区中可用的字节总数。 然后，可以使用 ODBC_INSTALL_COMPLETE *fRequest*和*cbPathOutMax*参数调用**sqlInstallDriverEx，** 该参数设置为*pcbPathOut*缓冲区中的值，以及 null 终止字符。  
  
 如果选择不将双相模型用于**SQLInstallDriverEx，** 则必须设置*cbPathOutMax*，该模型将目标目录路径的存储大小定义为 stdlib.h 中定义的值_MAX_PATH，以防止截断。  
  
 当*frequest* ODBC_INSTALL_COMPLETE时 **，SQLInstallDriverEx**不允许*lpszPathOut*为 NULL（或*cbPathOutMax*为 0）。 如果*fRequest*是ODBC_INSTALL_COMPLETE，则当可返回的字节数大于或等于*cbPathOutMax*时返回 FALSE，结果会出现截断。  
  
 在调用**SQLInstallDriverEx**并应用程序安装程序复制驱动程序文件（如有必要）后，驱动程序设置 DLL 必须调用**SQLConfigDriver**来设置驱动程序的配置。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|安装驱动程序管理器|[SQLInstall驱动程序管理器](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
