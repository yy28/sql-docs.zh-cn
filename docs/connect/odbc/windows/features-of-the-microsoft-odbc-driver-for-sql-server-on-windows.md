---
title: 在 Windows 上的 SQL Server 的 Microsoft ODBC 驱动程序的功能 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e2b7c107a40a60a1da5ed891d7a26a7c85011db
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="features-of-the-microsoft-odbc-driver-for-sql-server-on-windows"></a>Windows 上的 Microsoft ODBC Driver for SQL Server 的功能
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

    
## <a name="microsoft-odbc-driver-131-for-sql-server-on-windows"></a>Microsoft ODBC Driver 13.1 for Windows 上的 SQL Server

ODBC Driver 13.1 for SQL Server 包含以前的版本 (11) 的所有功能，并添加了对始终加密和 Azure Active Directory 身份验证，与 Microsoft SQL Server 2016 结合使用时支持。  
  
始终加密允许客户端对客户端应用程序内的敏感数据进行加密，并且永远不向 SQL Server 显示加密密钥。 安装在客户端计算机上的启用始终加密的驱动程序通过在 SQL Server 客户端应用程序中对敏感数据进行加密和解密来实现此目标。 该驱动程序先对敏感列中的数据进行加密，然后再将该数据传递到 SQL Server，并且自动重写查询以便保留应用程序的语义。 同样，该驱动程序以透明方式对存储在加密数据库列（包含在查询结果中）中的数据进行解密。 有关详细信息，请参阅[使用始终加密使用 ODBC 驱动程序](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)。
 
Azure Active Directory 允许用户，DBA 和应用程序程序员使用 Azure Active Directory 身份验证作为一种机制，通过使用在 Azure Active Directory (Azure AD 标识连接到 Microsoft Azure SQL 数据库和 Microsoft SQL Server 2016). 有关详细信息，请参阅[使用 Azure Active Directory 使用 ODBC 驱动程序](../../../connect/odbc/using-azure-active-directory.md)，和[连接到 SQL 数据库或 SQL 数据仓库使用 Azure Active Directory 身份验证](https://azure.microsoft.com/en-us/documentation/articles/sql-database-aad-authentication/)。   
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-windows"></a>Microsoft ODBC Driver 11 for SQL Server（Windows 平台）  

ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 包含 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 中随附的 [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]Native Client ODBC 驱动程序的所有功能。 有关详细信息，请参阅 [SQL Server Native Client 编程](http://msdn.microsoft.com/library/ms130892.aspx)。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client ODBC 驱动程序基于 Windows 操作系统中随附的 ODBC 驱动程序。 有关详细信息，请参阅 [Windows 数据访问组件 SDK](http://msdn.microsoft.com/library/aa968814(VS.85).aspx)。  
  
该版本的 ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 包含以下新功能：  
  
### <a name="bcpexe-l-option-for-specifying-a-login-timeout"></a>bcp.exe – l 选项用于指定登录超时值
 
– L 选项指定之前的秒数`bcp.exe`登录到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]当你尝试连接到服务器的超时。 默认登录超时值为 15 秒。 登录超时值必须是介于 0 和 65534 之间的数字。 如果提供的值不是数值或不在此范围内，则 `bcp.exe` 将生成错误消息。 值为 0 指定无限超时。 登录超时时间小于 （大约） 10 秒不可靠。  
  
### <a name="driver-aware-connection-pooling"></a>识别驱动程序的连接池  
ODBC Driver for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]支持[识别驱动程序的连接池](http://msdn.microsoft.com/library/hh405031(VS.85).aspx)。 有关详细信息，请参阅 [Driver-Aware Connection Pooling in the ODBC Driver for SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)。  
  
### <a name="asynchronous-execution-notification-method"></a>异步执行（通知方法）  
ODBC Driver for[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]支持[异步执行 （通知方法）](http://msdn.microsoft.com/library/hh405038(VS.85).aspx)。 有关用法示例，请参阅[异步执行&#40;通知方法&#41;示例](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)。  
  
### <a name="connection-resiliency"></a>连接复原
为了确保应用程序能与 Microsoft Azure SQL Database 保持连接，Windows 上的 ODBC 驱动程序可以还原空闲连接。 有关详细信息，请参阅 [Connection Resiliency in the Windows ODBC Driver](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)。  
  
## <a name="behavior-changes"></a>行为更改

在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]Native Client，`-y0`选项`sqlcmd.exe`导致输出被截断为 1 MB，如果显示 width 为 0。
  
从 ODBC Driver 11 for 开始[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]，可以在单个列中检索的数据量没有限制时`–y0`指定。 `sqlcmd.exe` 现在流式处理列至高达 2 GB ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]数据类型最大值)。  
  
另一个区别是该指定这两个`-h`和`-y0`现在会生成错误报告选项不兼容。 `-h`其中指定要在列标题之间打印的行数且从未与兼容`-y0`，尽管未不打印任何标题被忽略。
  
请注意，`-y0`可能对服务器和网络，具体取决于返回的数据大小会导致性能问题。

## <a name="see-also"></a>另请参阅  
[Microsoft ODBC Driver for SQL Server（Windows 平台）](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
