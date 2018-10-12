---
title: 连接到服务器 | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c251a239-e0bd-4f45-9207-b76651072dd0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 58357c0316f5b439d3dbac00a79547bd799e27bb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601955"
---
# <a name="connecting-to-the-server"></a>连接到服务器
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本部分中的主题介绍使用 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的选项和过程。  

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 可以使用 Windows 身份验证或使用 SQL Server 身份验证连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 默认情况下，[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 尝试使用 Windows 身份验证连接到服务器。  

## <a name="in-this-section"></a>本节内容  

|主题|描述|  
|---------|---------------|  
|[如何：使用 Windows 身份验证进行连接](../../connect/php/how-to-connect-using-windows-authentication.md)|介绍如何使用 Windows 身份验证建立连接。|  
|[如何：使用 SQL Server 身份验证进行连接](../../connect/php/how-to-connect-using-sql-server-authentication.md)|介绍如何使用 SQL Server 身份验证建立连接。|  
|[如何：使用 Azure Active Directory 身份验证进行连接](../../connect/php/azure-active-directory.md)|介绍如何设置身份验证模式，使用 Azure Active Directory 标识进行连接。|  
|[如何：在指定端口上连接](../../connect/php/how-to-connect-on-a-specified-port.md)|介绍如何在指定端口上连接到服务器。|  
|[连接池](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)|提供有关驱动程序中的连接池的信息。|  
|[如何：禁用多个活动的结果集 (MARS)](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)|介绍如何在建立连接时禁用 MARS 功能。|  
|[连接选项](../../connect/php/connection-options.md)|列出在包含连接属性的关联阵列中允许的选项。|  
|[支持 LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)|介绍对 LocalDB 功能的 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 支持，该支持已在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中添加。|  
|[支持高可用性、灾难恢复](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)|讨论如何配置应用程序以利用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中添加的高可用性和灾难恢复功能。|  
|[连接到 Microsoft Azure SQL 数据库](../../connect/php/connecting-to-microsoft-azure-sql-database.md)|讨论如何连接到 Azure SQL 数据库。|  
|[连接复原](../../connect/php/connection-resiliency.md)|讨论重新建立连接断开的连接复原功能。|  

## <a name="see-also"></a>另请参阅  
[适用于 SQL Server for PHP 编程 Microsoft 驱动程序的指南](../../connect/php/programming-guide-for-php-sql-driver.md)

[示例应用程序（SQLSRV 驱动程序）](../../connect/php/example-application-sqlsrv-driver.md)  
