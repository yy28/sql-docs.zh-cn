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
ms.openlocfilehash: 273633532b9b9247ea7aa12fe90bfcc3c6f6bb81
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083267"
---
# <a name="compatibility-matrix"></a>兼容性矩阵
下表描述了本部分前面定义的应用程序类型与驱动程序的兼容性。  
  
|应用程序类型<br /><br /> 和版本|32位 ODBC<br /><br /> 2.x*驱动程序*|ODBC *2.x*<br /><br /> 驱动器|ODBC 3.8 驱动程序|ISO 并打开与组兼容的驱动程序|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|16位应用程序，任何版本|兼容|兼容|兼容|兼容|  
|纯粹*的*2.x 应用程序|兼容|兼容|兼容|不兼容 [3]|  
|纯*2. x*重新编译的应用程序|兼容|兼容 [1]|兼容 [1]|不兼容 [3]|  
|纯*2. x* Unicode 应用程序|兼容|兼容 [1]|兼容 [1]|不兼容 [3]|  
|纯开放组和符合 ISO 标准的应用程序|不兼容|兼容 [2]|兼容 [2]|兼容 [2]|  
|纯3.0 应用程序|不兼容|兼容|兼容|不兼容 [4]|  
|纯3.5 应用程序|不兼容|兼容|兼容|不兼容 [4]|  
|纯3.8 （或更高版本）应用程序|不兼容 [5]|不兼容 [5]|兼容|不兼容 [4]|  
|已替换应用程序|兼容|兼容|兼容|不兼容 [3]|  
  
 [1] 应用程序必须使用 ODBC 3.5 （或更高版本）标头重新编译 UNICODE 选项（如果它是 Unicode 应用程序），并且必须将 ODBCVER 设置为0x0250。  
  
 [2] 应用程序必须使用 ODBC 3.5 （或更高版本）标头进行编译，并链接到 ODBC 驱动程序管理器。 它还必须设置标头标志 ODBC_STD。  
  
 [3] 此配置可能无法*工作，因为 ODBC 2.x*中有一些功能不符合标准，如书签。  
  
 [4] 此配置可能无法工作，*因为 ODBC 3.x 中的某些*功能不符合标准，如书签。  
  
 [5] 此配置可能会失败，因为 odbc 3.8 中的功能不在 odbc 2.x 或3.x 驱动程序中，如 ODBC 中特定于驱动程序的[C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
## <a name="driver-manager-compatibility"></a>驱动程序管理器兼容性  
 必须使用所有驱动程序管理器版本运行的 ODBC 3.0 应用程序应在启动时执行以下操作：  
  
-   分配环境句柄。  
  
-   将 SQL_ATTR_ODBC_VERSION 环境属性设置为 SQL_OV_ODBC3_80。 如果驱动程序管理器返回 SQL_ERROR，则驱动程序管理器将早于3.8。 根据需要重置 SQL_ATTR_ODBC_VERSION SQL_OV_ODBC3 或 SQL_OV_ODBC2，以对应于驱动程序管理器。  
  
-   分配连接句柄。  
  
-   建立连接。  
  
-   为 SQL_DRIVER_ODBC_VER 调用 SQLGetInfo 以确定驱动程序版本。 如果驱动程序是 ODBC 3.8 驱动程序，则可以使用特定于驱动程序的 C 类型。 否则，请不要使用驱动程序特定的 C 数据类型。  
  
 请注意，重新编译的 ODBC 1.x 应用程序可以使用除驱动程序特定的 C 类型之外的 ODBC 3.8 功能，而无需为 SQL_ATTR_ODBC_VERSION 指定 SQL_OV_ODBC3_80。 这类似于使用 ODBC 2.x 功能重新编译的 ODBC 2.x 应用程序。  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>在与所有驱动程序管理器兼容的应用程序中使用 SQLCancelHandle  
 由于在 Windows 7 之前发布的驱动程序管理器中不支持[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)，因此，如果应用程序直接调用**SQLCancelHandle** ，则无法在较旧版本的 Windows 中加载该应用程序。 若要使用驱动程序管理器的所有版本并在新版本的 Windows 上使用**SQLCancelHandle** ，应用程序应使用**LoadLibrary**和 GetProcAddress 间接调用**SQLCancelHandle** **。**  
  
## <a name="see-also"></a>另请参阅  
 [ODBC 3.8 中的新增功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
