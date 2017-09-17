---
title: "日志记录活动 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logging activity
ms.assetid: a777b3d9-2262-4e82-bc82-b62ad60d0e55
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d748bac061fdd4b76b1df0b9a6cf0a8101f21092
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="logging-activity"></a>日志记录活动
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

默认情况下，不会记录 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 生成的错误和警告。 本主题讨论如何配置日志记录活动。  
  
## <a name="logging-activity-using-the-pdosqlsrv-driver"></a>使用 PDO_SQLSRV 驱动程序的日志记录活动  
可用于 PDO_SQLSRV 驱动程序的唯一配置是 php.ini 文件中的 pdo_sqlsrv.log_severity 条目。  
  
在 php.ini 文件末尾添加以下内容：  
  
```  
[pdo_sqlsrv]  
pdo_sqlsrv.log_severity = <number>  
```  
  
**log_severity** 可以为下列值之一：  
  
|值|说明|  
|---------|---------------|  
|0|禁用日志记录（如果未进行任何定义，则为默认值）。|  
|-1|指定将记录错误、警告和通知。|  
|1|指定将记录错误。|  
|2|指定将记录警告。|  
|4|指定将记录通知。|  
  
日志记录信息将添加到 phperrors.log 文件。  
  
PHP 在初始化时读取配置文件并将数据存储在缓存中；它还提供一个 API 以更新这些设置并立即使用，然后它将写入配置文件。 此 API 支持应用程序脚本更改设置，即使在 PHP 初始化后也是如此。  
  
## <a name="logging-activity-using-the-sqlsrv-driver"></a>使用 SQLSRV 驱动程序的日志记录活动  
若要启用日志记录，可以使用 [sqlsrv_configure](../../connect/php/sqlsrv-configure.md) 函数，也可以修改 php.ini 文件。 你可以针对初始化、连接、语句或错误函数记录活动。 你还可以指定是记录错误、警告、通知还是同时记录这三者。  
  
> [!NOTE]  
> 可以在 php.ini 文件中配置日志文件的位置。  
  
### <a name="turning-logging-on"></a>启用日志记录  
你还可以使用 [sqlsrv_configure](../../connect/php/sqlsrv-configure.md) 函数为 **LogSubsystems** 设置指定一个值来启用日志记录。 例如，以下代码行配置驱动程序以针对连接记录活动：  
  
`sqlsrv_configure("LogSubsystems", SQLSRV_LOG_SYSTEM_CONN);`  
  
下表描述了可用作 **LogSubsystems** 设置的值的常量：  
  
|值（括号中为等效整数）|Description|  
|-----------------------------------------------|---------------|  
|SQLSRV_LOG_SYSTEM_ALL (-1)|对所有子系统启用日志记录。|  
|SQLSRV_LOG_SYSTEM_OFF (0)|禁用日志记录。 这是默认设置。|  
|SQLSRV_LOG_SYSTEM_INIT (1)|对初始化活动启用日志记录。|  
|SQLSRV_LOG_SYSTEM_CONN (2)|对连接活动启用日志记录。|  
|SQLSRV_LOG_SYSTEM_STMT (4)|对语句活动启用日志记录。|  
|SQLSRV_LOG_SYSTEM_UTIL (8)|对错误函数活动（例如 handle_error 和 handle_warning）启用日志记录。|  
  
你可以一次设置多个值**LogSubsystems**使用逻辑 OR 运算符 (|) 设置。 例如，以下代码行同时对连接和语句活动启用日志记录：  
  
`sqlsrv_configure("LogSubsystems", SQLSRV_LOG_SYSTEM_CONN | SQLSRV_LOG_SYSTEM_STMT);`  
  
你还可以通过在 php.ini 文件中为 **LogSubsystems** 设置指定整数值来启用日志记录。 例如，向 php.ini 文件中的 `[sqlsrv]` 部分添加以下行将对连接活动启用日志记录：  
  
`sqlsrv.LogSubsystems = 2`  
  
通过同时添加多个整数值，可以一次指定多个选项。 例如，向 php.ini 文件中的 `[sqlsrv]` 部分添加以下行将对连接和语句活动启用日志记录：  
  
`sqlsrv.LogSubsystems = 6`  
  
### <a name="logging-errors-warnings-and-notices"></a>记录错误、警告和通知  
启用日志记录后，必须指定要记录的内容。 你可以记录以下一个或多个类别：错误、警告和通知。 例如，以下代码行指定仅记录警告：  
  
`sqlsrv_configure("LogSeverity", SQLSRV_LOG_SEVERITY_WARNING);`  
  
> [!NOTE]  
> 默认设置**LogSeverity**是**SQLSRV_LOG_SEVERITY_ERROR**。 如果启用了日志记录，但未为 **LogSeverity** 指定任何设置，将仅记录错误。  
  
下表描述了可用作 **LogSeverity** 设置的值的常量：  
  
|值（括号中为等效整数）|Description|  
|-----------------------------------------------|---------------|  
|SQLSRV_LOG_SEVERITY_ALL (-1)|指定将记录错误、警告和通知。|  
|SQLSRV_LOG_SEVERITY_ERROR (1)|指定将记录错误。 这是默认设置。|  
|SQLSRV_LOG_SEVERITY_WARNING (2)|指定将记录警告。|  
|SQLSRV_LOG_SEVERITY_NOTICE (4)|指定将记录通知。|  
  
你可以一次设置多个值**LogSeverity**使用逻辑 OR 运算符 (|) 设置。 例如，以下代码行指定应记录错误和警告：  
  
`sqlsrv_configure("LogSeverity", SQLSRV_LOG_SEVERITY_ERROR | SQLSRV_LOG_SEVERITY_WARNING);`  
  
> [!NOTE]  
> 为 **LogSeverity** 设置指定值不会启用日志记录。 必须通过为 **LogSubsystems** 设置指定值来启用日志记录，然后通过为 **LogSeverity**设置值来指定所记录内容的级别。  
  
你还可以在 php.ini 文件中使用整数值来为 **LogSeverity** 设置指定一个设置。 例如，向 php.ini 文件中的 `[sqlsrv]` 部分添加以下行仅会对警告启用日志记录：  
  
`sqlsrv.LogSeverity = 2`  
  
通过同时添加多个整数值，可以一次指定多个选项。 例如，向 php.ini 文件中的 `[sqlsrv]` 部分添加以下行将对错误和警告启用日志记录：  
  
`sqlsrv.LogSeverity = 3`  
  
## <a name="see-also"></a>另请参阅  
[PHP SQL 驱动程序编程指南](../../connect/php/programming-guide-for-php-sql-driver.md)
[常量 &#40;Microsoft Drivers for PHP for SQL server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)  
[sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md)  
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  
  

