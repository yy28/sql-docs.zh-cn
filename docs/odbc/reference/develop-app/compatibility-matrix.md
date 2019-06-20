---
title: 兼容性矩阵 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application compatibility issues [ODBC]
- application upgrades [ODBC], compatibility matrix
- upgrading applications [ODBC], compatibility matrix
ms.assetid: 0690b463-15a1-48fa-9d0b-9cc9e5bf7fc6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b1d0fc510c7c45dab8fbc79cc8e74001ff1855b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63026570"
---
# <a name="compatibility-matrix"></a>兼容性矩阵
下表描述了应用程序和驱动程序之前在本部分中定义的类型的兼容性。  
  
|应用程序类型<br /><br /> 和版本|32 位 ODBC<br /><br /> 2.*x*驱动程序|ODBC 3.*x*<br /><br /> 驱动程序|ODBC 3.8 驱动程序|ISO 和打开组的兼容驱动程序|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|16 位应用程序，任何版本|兼容|兼容|兼容|兼容|  
|纯 2。*x*应用程序|兼容|兼容|兼容|Not compatible[3]|  
|纯 2。*x*重新编译应用程序|兼容|Compatible[1]|Compatible[1]|Not compatible[3]|  
|纯 2。*x* Unicode 应用程序|兼容|Compatible[1]|Compatible[1]|Not Compatible[3]|  
|纯打开组和符合 ISO 的应用程序|不兼容|Compatible[2]|Compatible[2]|Compatible[2]|  
|纯 3.0 应用程序|不兼容|兼容|兼容|Not compatible[4]|  
|纯 3.5 应用程序|不兼容|兼容|兼容|Not compatible[4]|  
|纯 3.8 （或更高版本） 的应用程序|不兼容 [5]|不兼容 [5]|兼容|不兼容 [4]|  
|被替换的应用程序|兼容|兼容|兼容|Not compatible[3]|  
  
 [1] 应用程序必须重新编译 （如果它是 Unicode 应用程序） 使用 UNICODE 选项使用 ODBC 3.5 （或更高版本） 标头并且必须设置为 0x0250 ODBCVER。  
  
 [2] 上，应用程序必须使用 ODBC 3.5 （或更高版本） 标头进行编译和链接使用 ODBC 驱动程序管理器。 它还必须设置的标头标志 ODBC_STD。  
  
 [3] 此配置可能可能无法工作，因为 ODBC 2 中有功能。*x*不标准，例如，书签中。  
  
 [4] 此配置可能无法工作，因为在 ODBC 3 有功能 *.x*不标准，例如，书签中。  
  
 [5] 此配置都有可能失败，因为不在 ODBC 2.x 或 3.x 驱动程序，例如特定于驱动程序符合 ODBC 3.8 中的功能[ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
## <a name="driver-manager-compatibility"></a>驱动程序管理器兼容性  
 必须运行的所有驱动程序管理器版本的 ODBC 3.0 应用程序应执行以下操作在启动：  
  
-   分配环境句柄。  
  
-   SQL_ATTR_ODBC_VERSION 环境属性设置为 SQL_OV_ODBC3_80。 如果驱动程序管理器将返回 SQL_ERROR，是早于 3.8 驱动程序管理器。 将重置 SQL_ATTR_ODBC_VERSION 为 SQL_OV_ODBC3 或 SQL_OV_ODBC2，根据需要，可对应到驱动程序管理器。  
  
-   分配连接句柄。  
  
-   建立连接。  
  
-   调用 SQLGetInfo 为 SQL_DRIVER_ODBC_VER 以确定驱动程序版本。 如果该驱动程序符合 ODBC 3.8 驱动程序，可以使用特定于驱动程序的 C 类型。 否则，不使用特定于驱动程序的 C 数据类型。  
  
 请注意，重新编译的 ODBC 3.x 应用程序可以使用 ODBC 3.8 功能不属于特定于驱动程序的 C 类型，而无需指定为 SQL_ATTR_ODBC_VERSION SQL_OV_ODBC3_80。 这是类似于使用 ODBC 3.x 功能的重新编译 ODBC 2.x 应用程序。  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>在应用程序更符合所有驱动程序管理器中使用 SQLCancelHandle  
 因为[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)不支持在 Windows 7 之前的版本发布的驱动程序管理器，应用程序不能加载较旧版本的 Windows 中如果它调用**SQLCancelHandle**直接。 若要使用的驱动程序管理器的所有版本和使用**SQLCancelHandle**在新版本的 Windows 中，应用程序应调用**SQLCancelHandle**间接通过使用**LoadLibrary**和**GetProcAddress。**  
  
## <a name="see-also"></a>请参阅  
 [ODBC 3.8 中的新增功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
