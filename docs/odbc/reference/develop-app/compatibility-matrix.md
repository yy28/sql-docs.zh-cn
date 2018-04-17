---
title: 兼容性矩阵 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application compatibility issues [ODBC]
- application upgrades [ODBC], compatibility matrix
- upgrading applications [ODBC], compatibility matrix
ms.assetid: 0690b463-15a1-48fa-9d0b-9cc9e5bf7fc6
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1199aab1324c086159fdbb83f111406a209a8e7b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="compatibility-matrix"></a>兼容性矩阵
下表描述的兼容性应用程序和驱动程序以前在本部分中定义的类型。  
  
|应用程序类型<br /><br /> 和版本|32 位 ODBC<br /><br /> 2.*x*驱动程序|ODBC 3。*x*<br /><br /> 驱动程序|ODBC 3.8 驱动程序|ISO 和打开组 – 符合驱动程序|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|16 位应用程序，任何版本|兼容|兼容|兼容|兼容|  
|纯 2。*x*应用程序|兼容|兼容|兼容|不兼容 [3]|  
|纯 2。*x*重新编译应用程序|兼容|兼容 [1]|兼容 [1]|不兼容 [3]|  
|纯 2。*x* Unicode 应用程序|兼容|兼容 [1]|兼容 [1]|不兼容 [3]|  
|纯打开组和 ISO – 符合应用程序|不兼容|兼容 [2]|兼容 [2]|兼容 [2]|  
|纯 3.0 的应用程序|不兼容|兼容|兼容|不兼容 [4]|  
|纯 3.5 应用程序|不兼容|兼容|兼容|不兼容 [4]|  
|纯 3.8 （或更高版本） 的应用程序|不兼容 [5]|不兼容 [5]|兼容|不兼容 [4]|  
|被替换的应用程序|兼容|兼容|兼容|不兼容 [3]|  
  
 [1] 应用程序必须重新编译 （如果它是 Unicode 应用程序） 使用 UNICODE 选项使用 ODBC 3.5 （或更高版本） 标头并且必须设置为 0x0250 的 ODBCVER。  
  
 [2] 上，应用程序必须使用 ODBC 3.5 （或更高版本） 标头进行编译和链接使用 ODBC 驱动程序管理器。 它还必须设置的标头标志 ODBC_STD。  
  
 [3] 此配置可能会失败以起作用，因为 ODBC 2 中有功能。*x*不标准，如书签中。  
  
 [4] 此配置可能会失败，以起作用，因为 ODBC 3 中有功能*.x*不标准，如书签中。  
  
 [5] 此配置可能会失败，因为没有 ODBC 3.8 不在 ODBC 2.x 或 3.x.驱动程序，例如特定于驱动程序的功能[ODBC 中的 C 数据类型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
## <a name="driver-manager-compatibility"></a>驱动程序管理器兼容性  
 必须运行的所有驱动程序管理器版本的 ODBC 3.0 应用程序应执行以下操作在启动时：  
  
-   分配的环境句柄。  
  
-   设置为 SQL_OV_ODBC3_80 SQL_ATTR_ODBC_VERSION 环境属性。 如果驱动程序管理器返回 SQL_ERROR，驱动程序管理器是早于 3.8。 将重置 SQL_ATTR_ODBC_VERSION 为 SQL_OV_ODBC3 或 SQL_OV_ODBC2，根据需要对应到驱动程序管理器。  
  
-   分配连接句柄。  
  
-   建立连接。  
  
-   调用 SQL_DRIVER_ODBC_VER 若要确定驱动程序版本的 SQLGetInfo。 如果 ODBC 3.8 驱动程序的驱动程序，则可以使用特定于驱动程序的 C 类型。 否则，不使用特定于驱动程序的 C 数据类型。  
  
 请注意，重新编译的 ODBC 3.x 应用程序可以使用 ODBC 3.8 功能以外的特定于驱动程序的 C 类型，而无需为 SQL_ATTR_ODBC_VERSION 指定 SQL_OV_ODBC3_80。 这是类似于使用 ODBC 3.x 功能的重新编译 ODBC 2.x 应用程序。  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>在应用程序更符合所有驱动程序管理器中使用 SQLCancelHandle  
 因为[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)不支持在 Windows 7 之前发布的驱动程序管理器中应用程序无法加载在较旧版本的 Windows 如果它调用**SQLCancelHandle**直接。 若要与所有版本的驱动程序管理器处理，并使用**SQLCancelHandle**在新版本的 Windows 中，应用程序应调用**SQLCancelHandle**间接通过使用**LoadLibrary**和**GetProcAddress。**  
  
## <a name="see-also"></a>另请参阅  
 [ODBC 3.8 中的新增功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
