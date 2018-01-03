---
title: "管理数据源 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deleting data sources [ODBC], ODBC data source administrator
- data sources [ODBC], ODBC data source administrator
- adding data sources [ODBC], ODBC data source administrator
- removing data sources [ODBC], ODBC data source administrator
- ODBC data source administrator [ODBC], data source management
ms.assetid: 67cc4945-4850-4eb4-8da6-b835ddaeca4c
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ea157fd72ab1cc2b37ba32e198bde5ff47eff0fb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="managing-data-sources"></a>管理数据源
从驱动程序的安装程序安装 ODBC 驱动程序后，你可以为它定义一个或多个数据源。 数据源名称 (DSN) 应提供数据; 的唯一的说明例如，*工资单*或*Accounts Payable*。 为所有当前安装的驱动程序定义的用户和系统数据源中列出**用户 DSN**或**系统 DSN**选项卡**ODBC 数据源管理器**对话框。 中列出给定目录中的文件数据源**文件 DSN**选项卡中输入要显示的目录**查找**框中**文件 DSN**选项卡。  
  
> [!NOTE]  
>  若要管理连接到在 64 位平台的 32 位驱动程序的数据源，请使用 c:\windows\sysWOW64\odbcad32.exe。 若要管理连接到 64 位驱动程序的数据源，请使用 c:\windows\system32\odbcad32.exe。 在**管理工具**在 64 位 Windows 8 操作系统系统中，有 32 位和 64 位的图标**ODBC 数据源管理器**对话框。  
  
 如果你使用 64 位 odbcad32.exe 配置或删除连接到 32 位驱动程序，例如的 DSN**驱动程序执行 Microsoft Access (\*.mdb)**，你将收到以下错误消息：  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 若要解决此错误，请使用 32 位 odbcad32.exe 要配置或删除 DSN。  
  
 数据源将特定的 ODBC 驱动程序与你想要通过该驱动程序访问的数据相关联。 例如，你可能创建数据源使用 ODBC dBASE 驱动程序来访问在您的硬盘或网络驱动器上的特定目录中找到的一个或多个 dBASE 文件。 使用 ODBC 数据源管理器，可以添加、 修改和删除数据源下, 表中所述。  
  
|操作|Description|  
|------------|-----------------|  
|添加数据源|它是可以添加多个数据源，每个将驱动程序与你想要使用该驱动程序访问某些数据相关联。 为每个数据源指定唯一标识该数据源的名称。 例如，如果你创建包含客户信息的 dBASE 文件的一组的数据源，你可以命名数据源"Customers。 应用程序通常显示用户从中选择的数据源的名称。<br /><br /> 添加文件数据源是与添加用户或系统数据源略有不同。 有关详细信息，请参阅 ODBC 数据源管理器帮助文件。|  
|修改数据源|具体取决于你的要求，您可能发现不必重新配置数据源。 可以通过单击重置选项**配置**任何驱动程序安装程序对话框中。|  
|删除数据源|单击**删除**后选择的数据源。|  
  
 有关文件数据源的详细信息，请参阅[连接使用的文件数据源](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)或[SQLDriverConnect 函数](../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC 数据源管理器](../../odbc/admin/odbc-data-source-administrator.md)
