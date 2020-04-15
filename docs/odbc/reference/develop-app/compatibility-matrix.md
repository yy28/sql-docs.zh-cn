---
title: 兼容性矩阵 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0406599e1657a900d1669861572ff13834cec670
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307450"
---
# <a name="compatibility-matrix"></a>兼容性矩阵
下表描述了本节中前面定义的应用程序和驱动程序类型的兼容性。  
  
|应用程序类型<br /><br /> 和版本|32 位 ODBC<br /><br /> *2.x*驱动程序|ODBC *3.x*<br /><br /> 驱动程序|ODBC 3.8 驱动程序|符合 ISO 和打开组的驱动程序|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|16 位应用程序，任何版本|兼容|兼容|兼容|兼容|  
|纯*2.x*应用|兼容|兼容|兼容|不兼容[3]|  
|纯*2.x*重新编译的应用程序|兼容|兼容[1]|兼容[1]|不兼容[3]|  
|纯*2.x* Unicode 应用程序|兼容|兼容[1]|兼容[1]|不兼容[3]|  
|纯开放组和符合 ISO 的应用程序|不兼容|兼容[2]|兼容[2]|兼容[2]|  
|纯 3.0 应用|不兼容|兼容|兼容|不兼容[4]|  
|纯 3.5 应用|不兼容|兼容|兼容|不兼容[4]|  
|纯 3.8（或更高）应用|不兼容 [5]|不兼容 [5]|兼容|不兼容 [4]|  
|替换应用程序|兼容|兼容|兼容|不兼容[3]|  
  
 [1] 应用程序必须使用具有 UNICODE 选项（如果是 Unicode 应用程序）的 ODBC 3.5（或更高）标头重新编译，并且必须将 ODBCVER 设置为 0x0250。  
  
 [2] 应用程序必须使用 ODBC 3.5（或更高）标头进行编译，并与 ODBC 驱动程序管理器链接。 它还必须ODBC_STD设置标题标志。  
  
 [3] 此配置可能不起作用，因为 ODBC *2.x*中有些功能不在标准中，例如书签。  
  
 [4] 此配置可能不起作用，因为 ODBC *3.x*中有些功能不在标准中，例如书签。  
  
 [5] 此配置可能会失败，因为 ODBC 3.8 中有些功能不在 ODBC 2.x 或 3.x 驱动程序中，例如[ODBC 中](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)特定于驱动程序的 C 数据类型。  
  
## <a name="driver-manager-compatibility"></a>驱动程序管理器兼容性  
 必须在所有驱动程序管理器版本操作的 ODBC 3.0 应用程序应在启动时执行以下操作：  
  
-   分配环境句柄。  
  
-   将SQL_ATTR_ODBC_VERSION环境属性设置为SQL_OV_ODBC3_80。 如果驱动程序管理器返回SQL_ERROR，则驱动程序管理器大于 3.8。 根据需要将SQL_ATTR_ODBC_VERSION重置为SQL_OV_ODBC3或SQL_OV_ODBC2，以便与驱动程序管理器相对应。  
  
-   分配连接句柄。  
  
-   建立连接。  
  
-   调用 SQLGetInfo 进行SQL_DRIVER_ODBC_VER以确定驱动程序版本。 如果驱动程序是 ODBC 3.8 驱动程序，则可以使用特定于驱动程序的 C 类型。 否则，不要使用特定于驱动程序的 C 数据类型。  
  
 请注意，重新编译的 ODBC 3.x 应用程序可以使用特定于驱动程序的 C 类型以外的 ODBC 3.8 功能，而无需为SQL_ATTR_ODBC_VERSION指定SQL_OV_ODBC3_80。 这与使用 ODBC 3.x 功能重新编译的 ODBC 2.x 应用程序类似。  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>在与所有驱动程序管理器兼容的应用程序中使用 SQLCancelHandle  
 由于在 Windows 7 之前发布的驱动程序管理器中不支持[SQLCancelHandle 函数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)，因此如果应用程序直接调用**SQLCancelHandle，** 则无法在旧版本的 Windows 中加载它。 要使用所有版本的驱动程序管理器并在新版本的 Windows 上使用**SQLCancelHandle，** 应用程序应使用**LoadLibrary**和**GetProcAddress**间接调用**SQLCancelHandle。**  
  
## <a name="see-also"></a>另请参阅  
 [ODBC 3.8 中的新增功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
