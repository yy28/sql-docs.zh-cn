---
title: SQLInstallDriverEx 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b6bae692efdb1d89642eea52e499b0fb2800377
ms.sourcegitcommit: fc6a6eedcea2d98c93e33d39c1cecd99fbc9a155
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2018
ms.locfileid: "49169313"
---
# <a name="sqlinstalldriverex-function"></a>SQLInstallDriverEx 函数
**符合性**  
 版本引入了： ODBC 3.0  
  
 **摘要**  
 **SQLInstallDriverEx**将驱动程序有关的信息添加到 Odbcinst.ini 条目中的系统信息和递增的驱动程序*UsageCount* 1。 但是，如果版本的驱动程序已存在，但*UsageCount*驱动程序不存在，值的新*UsageCount*值设置为 2。  
  
 此函数不会实际复制的任何文件。 它负责的调用程序将正确的驱动程序文件复制到目标目录。  
  
 功能**SQLInstallDriverEx**还可以访问与[ODBCCONF。EXE](../../../odbc/odbcconf-exe.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
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
 [输入]驱动程序的描述 （通常关联 DBMS 的名称） 提供给用户而不是物理驱动器的名称。 *LpszDriver*参数必须包含描述该驱动程序的关键字 / 值对的双向以 null 结尾的列表。 有关关键字值对的详细信息，请参阅[驱动程序规范子项](../../../odbc/reference/install/driver-specification-subkeys.md)。 有关双向以 null 结尾的字符串的详细信息，请参阅[ConfigDSN 函数](../../../odbc/reference/syntax/configdsn-function.md)。  
  
 *lpszPathIn*  
 [输入]安装过程中或为 null 指针的目标目录的完整路径。 如果*lpszPathIn*是 null 指针，将在系统目录中安装了驱动程序。  
  
 *lpszPathOut*  
 [输出]应安装驱动程序的目标目录的路径。 如果以前尚未安装该驱动程序， *lpszPathOut*应与相同*lpszPathIn*。 如果之前安装该驱动程序， *lpszPathOut*是以前安装的路径。  
  
 *cbPathOutMax*  
 [输入]长度*lpszPathOut*。  
  
 *pcbPathOut*  
 [输出]总 （不包括 null 终止字符） 的字节数可用于在中返回*lpszPathOut*。 可用来返回的字节数是否大于或等于*cbPathOutMax*中的输出路径*lpszPathOut*将被截断为*cbPathOutMax*减null 终止字符。 *PcbPathOut*参数可以是 null 指针。  
  
 *fRequest*  
 [输入]请求的类型。 *FRequest*参数必须包含以下值之一：  
  
 ODBC_INSTALL_INQUIRY： 查询有关安装驱动程序的位置。  
  
 ODBC_INSTALL_COMPLETE： 完成安装请求。  
  
 *lpdwUsageCount*  
 [输出]驱动程序后调用此函数的使用情况计数。  
  
 应用程序不应设置的使用计数。 ODBC 将保持此计数。  
  
## <a name="returns"></a>返回  
 如果成功，则返回 FALSE 出现故障时，该函数返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLInstallDriverEx**返回 FALSE，关联 *\*pfErrorCode*可以通过调用获取的值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|出错的其中没有特定的安装程序错误。|  
|ODBC_ERROR_INVALID_BUFF_LEN|无效缓冲区长度|*LpszPathOut*参数不是足够大以包含输出路径。 在缓冲区中包含的被截断的路径。<br /><br /> *CbPathOutMax*参数为 0，并且*fRequest*已 ODBC_INSTALL_COMPLETE。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|请求的类型无效|*FRequest*参数不是以下之一：<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|无效的关键字值对|*LpszDriver*参数包含语法错误。|  
|ODBC_ERROR_INVALID_PATH|无效的安装路径|*LpszPathIn*参数包含无效的路径。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|无法加载驱动程序或转换器安装程序库|无法加载驱动程序安装程序库。|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|无效的参数序列|*LpszDriver*参数不包含一系列关键字值对。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|无法递增或递减的组件使用计数|安装程序无法递增驱动程序的使用情况计数。|  
  
## <a name="comments"></a>注释  
 *LpszDriver*参数是中的关键字值对形式的属性列表。 每个对终止 null 字节，并且整个列表终止 null 字节。 （也就是说，两个 null 字节标记列表的末尾。）此列表的格式如下所示：  
  
 _驱动程序 desc_ **\\**0Driver**=**_驱动程序 DLL 文件名_**\\**0 [安装程序**=**_安装程序 DLL 文件名_<b>\\</b>0]  
  
 [_驱动程序 attr keyword1_**=**_value1_<b>\\</b>0] [_驱动程序 attr keyword2_ **=** _value2_<b>\\</b>0]...<b> \\ </b>0  
  
 其中 \0 是 null 字节和*驱动程序 attr keywordn*是任何驱动程序属性关键字。 关键字必须出现在指定的顺序。 例如，假设用于格式化的文本的文件的驱动程序具有单独的驱动程序和安装程序 Dll，并可以使用具有.txt 和.csv 扩展名的文件。 *LpszDriver*此驱动程序的参数可能按如下所示：  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 假设 SQL Server 驱动程序不具有单独的安装程序 DLL，不具有任何驱动程序属性关键字。 *LpszDriver*此驱动程序的参数可能按如下所示：  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 之后**SQLInstallDriverEx**检索中的驱动程序有关的信息*lpszDriver*参数，它添加到 Odbcinst.ini 条目的 [ODBC Drivers] 部分系统中的驱动程序说明信息。 然后创建与驱动程序的说明一节，并将驱动程序 DLL 的完整路径和安装程序 DLL 添加。 最后，它返回安装在目标目录的路径，但不会将驱动程序文件复制到它。 实际上，调用程序必须将驱动程序文件复制到目标目录。  
  
 **SQLInstallDriverEx**安装的驱动程序的组件使用计数递增 1。 如果版本的驱动程序已存在，但该驱动程序的组件使用计数不存在，则会将新组件使用情况计数值设置为 2。  
  
 应用程序安装程序是负责以物理方式将驱动程序文件复制和维护文件使用情况计数。 如果以前尚未安装驱动程序文件，应用程序安装程序必须将复制的文件中*lpszPathIn*路径和创建文件使用情况计数。 如果文件先前已安装，安装程序只是递增文件使用情况计数并返回以前安装的路径*lpszPathOut*参数。  
  
> [!NOTE]  
>  有关组件使用计数和文件使用情况计数的详细信息，请参阅[使用情况计数](../../../odbc/reference/install/usage-counting.md)。  
  
 如果应用程序之前安装驱动程序文件的较旧版本，该驱动程序应为卸载并再重新安装，以使驱动程序组件的使用情况计数有效。 **SQLConfigDriver** (使用*fRequest* ODBC_REMOVE_DRIVER 的) 应首次调用，然后**SQLRemoveDriver**应调用要递减的组件使用计数。 **SQLInstallDriverEx**然后应调用以重新安装驱动程序，递增的组件使用计数。 应用程序安装程序必须使用新文件替换旧的文件。 文件使用情况计数将保持不变，并使用较早的版本文件的任何其他应用程序现在将使用较新版本。  
  
> [!NOTE]  
>  如果以前安装了驱动程序和**SQLInstallDriverEx**称为驱动程序安装在不同的目录，该函数将返回 TRUE，但*lpszPathOut*将包含目录其中已安装该驱动程序。 它不会在输入的目录*lpszDriver*参数。  
  
 中的路径的长度*lpszPathOut*中**SQLInstallDriverEx**允许对两阶段的安装过程，因此应用程序可以确定什么*cbPathOutMax*应通过调用**SQLInstallDriverEx**与*fRequest* ODBC_INSTALL_INQUIRY 模式。 这将返回中可用的字节总数*pcbPathOut*缓冲区。 **SQLInstallDriverEx**然后可以使用调用*fRequest* ODBC_INSTALL_COMPLETE 的并且*cbPathOutMax*参数设置中的值为*pcbPathOut*缓冲区，再加上 null 终止字符。  
  
 如果您选择不使用的两阶段模型**SQLInstallDriverEx**，则必须设置*cbPathOutMax*，其定义的到值 _MAX_PATH 的目标目录的路径的存储大小为在 Stdlib.h 中定义，以防止发生截断。  
  
 当*fRequest*是 ODBC_INSTALL_COMPLETE， **SQLInstallDriverEx**不允许*lpszPathOut*为 NULL (或*cbPathOutMax*为0)。 如果*fRequest* ODBC_INSTALL_COMPLETE，则返回 FALSE 时，将返回可用于返回的字节数是大于或等于*cbPathOutMax*，与结果发生截断。  
  
 之后**SQLInstallDriverEx**已调用和应用程序安装程序已复制的驱动程序文件 （如有必要），驱动程序安装程序必须调用 DLL **SQLConfigDriver**若要设置的配置驱动程序。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|安装驱动程序管理器|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
