---
title: ODBC Linux 和 macOS 的常见问题解答 (FAQ) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 65bfd6d2-c83d-4528-a5e1-a85b125a4f4a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17d25f6084e136736dbc4c8a8ff3cb019ce4692e
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37991369"
---
# <a name="frequently-asked-questions-faq-for-odbc-linux-and-macos"></a>ODBC Linux 和 macOS 的常见问题解答 (FAQ)
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

以下是有关 Linux 和 macOS 上的 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 的问题解答。
  
## <a name="frequently-asked-questions"></a>常见问题

**Linux 或 macOS 上的现有 ODBC 应用程序如何使用该驱动程序？**  
你应该能够编译并运行已使用其他驱动程序在 Linux 或 macOS 上编译并运行的 ODBC 应用程序。 
  
**此版本的驱动程序支持 [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] 的哪些功能？**

Linux 和 macOS 上的 ODBC 驱动程序支持 [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] 中除 LocalDB 以外的所有服务器功能。 有关详细信息[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]支持的功能，请参阅[Programming Guidelines](../../../connect/odbc/linux-mac/programming-guidelines.md)。  
  
**该驱动程序是否支持 Kerberos 身份验证？**  
是。 如果有现有的 Kerberos 环境设置，您应能够连接到服务器使用`Trusted_Connection=Yes`DSN 或连接字符串选项。 有关详细信息，请参阅[使用集成身份验证](../../../connect/odbc/linux-mac/using-integrated-authentication.md)。  
  
**应用程序应使用哪种 Unicode 编码？**  
为 SQL_CHAR 数据使用 UTF-8，为 SQL_WCHAR 数据使用 UTF-16。  

**是否提供可下载并通过该驱动程序运行以对其进行体验和评估的 ODBC 示例？**

请参阅 [使用 Linux 上的 ODBC 驱动程序的现有 MSDN C++ ODBC 示例](http://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) 以获取示例。 这也是适用于 macOS 的 ODBC 驱动程序。 

**Linux 上的 ODBC 驱动程序还是 macOS 开放源代码？**

否，Linux 和 macOS 上的 ODBC 驱动程序不是一个开放源产品。  

## <a name="see-also"></a>另请参阅
[在 Linux 和 macOS 上安装 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
