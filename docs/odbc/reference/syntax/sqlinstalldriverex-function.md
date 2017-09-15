---
title: "SQLInstallDriverEx 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2eda9fe4e6a5f300f83512f669ad5206f89effe6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlinstalldriverex-function"></a>SQLInstallDriverEx 函数
**一致性**  
 版本引入了： ODBC 3.0  
  
 **摘要**  
 **SQLInstallDriverEx**将驱动程序的信息添加到中的系统信息的 Odbcinst.ini 条目，并增加驱动程序的*UsageCount* 1。 但是，如果的版本的驱动程序已存在但*UsageCount*值不存在该驱动程序，新*UsageCount*值设置为 2。  
  
 此函数实际上不复制任何文件。 它是调用程序正确将驱动程序的文件复制到目标目录的责任。  
  
 功能**SQLInstallDriverEx**还可通过访问[ODBCCONF。EXE](../../../odbc/odbcconf-exe.md)。  
  
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
 [输入]驱动程序说明 （通常名称关联的 DBMS） 呈现给用户，而不是物理驱动器的名称。 *LpszDriver*自变量必须包含双向以 null 结尾的关键字 / 值对描述该驱动程序列表。 有关关键字 / 值对的详细信息，请参阅[驱动程序规范子项](../../../odbc/reference/install/driver-specification-subkeys.md)。 有关的双向以 null 结尾的字符串的详细信息，请参阅[ConfigDSN 函数](../../../odbc/reference/syntax/configdsn-function.md)。  
  
 *lpszPathIn*  
 [输入]安装或 null 指针的目标目录的完整路径。 如果*lpszPathIn*是 null 指针，将在系统目录中安装了驱动程序。  
  
 *lpszPathOut*  
 [输出]应安装驱动程序的目标目录的路径。 如果以前尚未安装该驱动程序， *lpszPathOut*应为相同*lpszPathIn*。 如果以前安装了驱动程序， *lpszPathOut*是以前安装的路径。  
  
 *cbPathOutMax*  
 [输入]长度*lpszPathOut*。  
  
 *pcbPathOut*  
 [输出]总字节数 （不包括 null 终止字符） 可用于返回在*lpszPathOut*。 可用于返回的字节数是否大于或等于*cbPathOutMax*中的输出路径*lpszPathOut*截断为*cbPathOutMax*减null 终止字符。 *PcbPathOut*参数可以是 null 指针。  
  
 *fRequest*  
 [输入]请求的类型。 *FRequest*参数必须包含以下值之一：  
  
 ODBC_INSTALL_INQUIRY： 查询可以在其中安装了驱动程序。  
  
 ODBC_INSTALL_COMPLETE： 完成了安装请求。  
  
 *lpdwUsageCount*  
 [输出]在调用此函数后的驱动程序使用情况计数。  
  
 应用程序不应设置的使用计数。 ODBC 将维护此计数。  
  
## <a name="returns"></a>返回  
 如果它成功，则返回 FALSE 如果失败，则函数将返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLInstallDriverEx**返回 FALSE，一个关联* \*pfErrorCode*可通过调用获取值**SQLInstallerError**。 下表列出* \*pfErrorCode*可以返回的值**SQLInstallerError**并解释此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|对于发生了错误其中没有任何特定的安装程序错误。|  
|ODBC_ERROR_INVALID_BUFF_LEN|无效的缓冲区长度|*LpszPathOut*自变量不为大到足以包含的输出路径。 在缓冲区中包含的截断的路径。<br /><br /> *CbPathOutMax*自变量为 0，和*fRequest*已 ODBC_INSTALL_COMPLETE。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|请求的类型无效|*FRequest*自变量不是以下之一：<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|无效的关键字 / 值对|*LpszDriver*参数包含语法错误。|  
|ODBC_ERROR_INVALID_PATH|无效的安装路径|*LpszPathIn*参数包含无效的路径。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|无法加载驱动程序或转换器安装库|无法加载驱动程序安装程序库。|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|无效的参数序列|*LpszDriver*自变量不包含的关键字 / 值对的列表。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|无法递增或递减的组件使用计数|安装程序无法递增驱动程序的使用情况计数。|  
  
## <a name="comments"></a>注释  
 *LpszDriver*自变量是中的关键字 / 值对形式的属性列表。 每个对终止与 null 字节，并且整个列表因 null 字节。 （也就是说，两个 null 字节标记列表的末尾。）此列表的格式如下所示：  
  
 *驱动程序 desc* ** \\ **0Driver**=***驱动程序 DLL 文件名*** \\ **0 [安装程序**=***安装程序 DLL filename***\\**0]  
  
 [*驱动程序 attr keyword1***=***value1***\\**0] [*驱动程序 attr keyword2* ** = ** *value2***\\**0]...** \\ **0  
  
 其中 \0 是 null 字节和*驱动程序 attr keywordn*是任何驱动程序属性关键字。 关键字必须出现在指定的顺序。 例如，假设的驱动程序格式化的文本文件具有单独的驱动程序和安装程序 Dll，并且可以使用具有.txt 和.csv 扩展名的文件。 *LpszDriver*此驱动程序的自变量可能，如下所示：  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 假设 SQL Server 的驱动程序不具有单独的安装程序 DLL，并且没有任何驱动程序属性关键字。 *LpszDriver*此驱动程序的自变量可能，如下所示：  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 后**SQLInstallDriverEx**检索从驱动程序有关的信息*lpszDriver*自变量，它添加到 Odbcinst.ini 条目的 [ODBC 驱动程序] 部分系统中的驱动程序说明信息。 然后，它将创建标题为驱动程序的说明所含的区段，并添加的驱动程序 DLL 的完整路径，然后安装程序 DLL。 最后，它返回目标安装目录的路径，但不会复制到该驱动程序文件。 实际上，调用程序必须将驱动程序文件复制到目标目录。  
  
 **SQLInstallDriverEx**安装的驱动程序的组件使用计数递增 1。 如果驱动程序的版本已存在，但该驱动程序的组件使用计数不存在，则会将新组件使用情况计数值设置为 2。  
  
 应用程序安装程序负责以物理方式将驱动程序文件复制和维护的文件使用计数。 如果以前尚未安装驱动程序文件，应用程序安装程序必须将复制的文件中*lpszPathIn*路径和创建的文件使用计数。 如果以前已安装文件，安装程序只是文件使用情况计数递增 1 并将返回中的以前安装的路径*lpszPathOut*自变量。  
  
> [!NOTE]  
>  有关组件使用计数和文件的使用情况计数的详细信息，请参阅[使用情况计数](../../../odbc/reference/install/usage-counting.md)。  
  
 如果驱动程序文件的旧版本以前已安装应用程序，则应卸载该驱动程序，并将其然后重新安装，以使驱动程序组件使用率计数有效。 **SQLConfigDriver** (与*fRequest*的 ODBC_REMOVE_DRIVER) 应首先调用，然后**SQLRemoveDriver**应调用以减少的组件使用情况计数。 **SQLInstallDriverEx**然后应调用以重新安装驱动程序，递增的组件使用计数。 应用程序安装程序必须使用新的文件替换旧的文件。 文件使用情况计数将保持不变，并使用较旧版本文件的任何其他应用程序现在将使用较新版本。  
  
> [!NOTE]  
>  如果以前安装了驱动程序和**SQLInstallDriverEx**调用以安装驱动程序在不同的目录，该函数将返回 TRUE，但*lpszPathOut*将包含目录其中已安装该驱动程序。 它不包含输入中的目录*lpszDriver*自变量。  
  
 中的路径的长度*lpszPathOut*中**SQLInstallDriverEx**允许对于的两阶段安装进程，因此应用程序可以确定什么*cbPathOutMax*应通过调用**SQLInstallDriverEx**与*fRequest*的 ODBC_INSTALL_INQUIRY 模式。 这将返回中可用的字节总数*pcbPathOut*缓冲区。 **SQLInstallDriverEx**然后可以使用调用*fRequest*的 ODBC_INSTALL_COMPLETE 和*cbPathOutMax*参数设置中的值为*pcbPathOut*缓冲区，加上的 null 终止字符。  
  
 如果你选择不使用的两阶段模型**SQLInstallDriverEx**，必须设置*cbPathOutMax*，其定义为值 _MAX_PATH，到的目标目录的路径的存储大小定义在 Stdlib.h 中以防止发生截断。  
  
 当*fRequest*是 ODBC_INSTALL_COMPLETE， **SQLInstallDriverEx**不允许*lpszPathOut*为 NULL (或*cbPathOutMax*要0)。 如果*fRequest* ODBC_INSTALL_COMPLETE，如果可用于返回的字节数大于或等于 FALSE 则返回*cbPathOutMax*，使用结果进行该截断。  
  
 后**SQLInstallDriverEx**已调用和应用程序安装程序已复制的驱动程序文件 （如有必要）、 驱动程序安装程序必须调用 DLL **SQLConfigDriver**设置的配置驱动程序。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|安装驱动程序管理器|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
