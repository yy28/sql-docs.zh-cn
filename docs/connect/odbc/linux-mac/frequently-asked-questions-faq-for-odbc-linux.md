---
title: "常见问题 (FAQ) 适用于 ODBC Linux 和 macOS |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 65bfd6d2-c83d-4528-a5e1-a85b125a4f4a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: aa835ce2bb9e35191d9c3056dad2f208445c361a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="frequently-asked-questions-faq-for-odbc-linux-and-macos"></a>常见问题 (FAQ) 适用于 ODBC Linux 和 macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

以下是有关 ODBC 驱动程序有关的问题的答案[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]在 Linux 和 macOS 上。
  
## <a name="frequently-asked-questions"></a>常见问题

**Linux 或 macOS 上的现有 ODBC 应用程序使用该驱动程序？**  
你应能够编译和运行的 ODBC 应用程序，你已编译并在 Linux 或 macOS 使用其他驱动程序上运行。 
  
**功能[!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]驱动程序支持此版本？**

在 Linux 和 macOS 上的 ODBC 驱动程序支持中的所有服务器功能[!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]除 LocalDB 以外。 有关详细信息[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]支持的功能，请参阅[编程准则](../../../connect/odbc/linux-mac/programming-guidelines.md)。  
  
**该驱动程序是否支持 Kerberos 身份验证？**  
是。 如果你有现有的 Kerberos 环境设置，你应能够连接到服务器使用`Trusted_Connection=Yes`DSN 或连接字符串选项。 有关详细信息，请参阅[使用集成身份验证](../../../connect/odbc/linux-mac/using-integrated-authentication.md)。  
  
**哪种 Unicode 编码应用程序应使用？**  
为 SQL_CHAR 数据使用 UTF-8，为 SQL_WCHAR 数据使用 UTF-16。  

**是否有我可以下载并使用要试用或评估它的驱动程序运行的 ODBC 示例？**

请参阅 [使用 Linux 上的 ODBC 驱动程序的现有 MSDN C++ ODBC 示例](http://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) 以获取示例。 这也是适用于 macOS ODBC 驱动程序。 

**在 Linux 上的 ODBC 驱动程序或 macOS 打开源？**

否，在 Linux 和 macOS 上的 ODBC 驱动程序不是开源产品。  

## <a name="see-also"></a>另请参阅
[安装 Microsoft ODBC Driver for SQL Server 在 Linux 和 macOS 上](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

