---
title: "PHP SQL 驱动程序的安全注意事项 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security considerations
ms.assetid: a8c1a570-9204-454f-b94c-ba34f54d487c
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2a7423bcfcfd28073840ad7f8c9ee2e7424507bc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="security-considerations-for-php-sql-driver"></a>PHP SQL 驱动程序的安全注意事项
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主题介绍特定于开发、部署和运行使用 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的应用程序的安全注意事项。 有关 SQL Server 安全性的更多详细信息，请参阅 [数据安全性与合规性](http://go.microsoft.com/fwlink/?LinkId=129225)。  
  
## <a name="connect-using-windows-authentication"></a>使用 Windows 身份验证进行连接  
只要可能存在以下原因，都应使用 Windows 身份验证来连接 SQL Server：  
  
-   **在身份验证过程中，未通过网络传递任何凭据。** 用户名和密码未嵌入在数据库连接字符串中。 这意味着恶意用户或攻击者无法通过监视网络或查看配置文件内部的连接字符串来获取凭据。  
  
-   **用户要进行集中式帐户管理。** 强制执行多次无效登录请求后的安全策略，如密码有效期、最短密码长度和帐户锁定。  
  
有关如何使用 Windows 身份验证连接到服务器的信息，请参阅 [如何：使用 Windows 身份验证进行连接](../../connect/php/how-to-connect-using-windows-authentication.md)。  
  
使用 Windows 身份验证进行连接时，建议你配置环境，以便 SQL Server 可以使用 Kerberos 身份验证协议。 有关详细信息，请参阅 [如何确保在创建到 SQL Server 2005 实例的远程连接时使用 Kerberos 身份验证](http://go.microsoft.com/fwlink/?LinkId=121862) 或 [Kerberos 身份验证与 SQL Server](http://go.microsoft.com/fwlink/?LinkId=129226)。  
  
## <a name="use-encrypted-connections-when-transferring-sensitive-data"></a>在传输敏感数据时使用加密连接  
无论通过 SQL Server 发送还是接收敏感数据，都应使用加密连接。 有关如何启用加密的连接的信息，请参阅[如何启用到数据库引擎 （SQL Server 配置管理器） 的加密连接](http://go.microsoft.com/fwlink/?LinkId=121864)。 若要与 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]建立安全连接，请在连接到服务器时使用加密连接属性。 有关连接属性的详细信息，请参阅 [Connection Options](../../connect/php/connection-options.md)。  
  
## <a name="use-parameterized-queries"></a>使用参数化查询  
使用参数化查询降低 SQL 注入攻击的风险。 有关执行参数化查询的示例，请参阅 [How to: Perform Parameterized Queries](../../connect/php/how-to-perform-parameterized-queries.md)。  
  
有关 SQL 注入攻击的详细信息以及相关安全注意事项，请参阅 [SQL 注入](http://go.microsoft.com/fwlink/?LinkId=104224)。  
  
## <a name="do-not-accept-server-or-connection-string-information-from-end-users"></a>不要从最终用户接受服务器或连接字符串信息  
编写应用程序，以使最终用户无法将服务器或连接字符串信息提交到应用程序。 维持对服务器和连接字符串信息的严格控制可减少恶意活动的外围应用。  
  
## <a name="turn-warningsaserrors-on-during-application-development"></a>在应用程序开发期间启用 WarningsAsErrors  
在开发应用程序期间，将 **WarningsAsErrors** 设置设为 **True** ，以便将驱动程序发出的警告视为错误。 这将允许你在部署应用程序之前处理警告。 有关详细信息，请参阅 [Handling Errors and Warnings](../../connect/php/handling-errors-and-warnings.md)。  
  
## <a name="secure-logs-for-deployed-application"></a>已部署应用程序的安全日志  
对于已部署的应用程序，请确保日志写入安全位置或关闭日志记录。 这有助于防止最终用户可能访问已写入日志文件的信息。 有关详细信息，请参阅 [Logging Activity](../../connect/php/logging-activity.md)。  
  
## <a name="see-also"></a>另请参阅  
[PHP SQL 驱动程序编程指南](../../connect/php/programming-guide-for-php-sql-driver.md)
  

