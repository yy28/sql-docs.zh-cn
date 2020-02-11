---
title: 管理数据源 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- deleting data sources [ODBC], ODBC data source administrator
- data sources [ODBC], ODBC data source administrator
- adding data sources [ODBC], ODBC data source administrator
- removing data sources [ODBC], ODBC data source administrator
- ODBC data source administrator [ODBC], data source management
ms.assetid: 67cc4945-4850-4eb4-8da6-b835ddaeca4c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9dc741321894ae69a9ffb59738576a01d47628f5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67901661"
---
# <a name="managing-data-sources"></a>管理数据源
从驱动程序的安装程序安装了 ODBC 驱动程序后，可以为其定义一个或多个数据源。 数据源名称（DSN）应提供数据的唯一说明;例如，*工资单*或*应付帐款*。 为所有当前安装的驱动程序定义的用户和系统数据源列在 " **ODBC 数据源管理器**" 对话框的 "**用户 dsn** " 或 "**系统 dsn** " 选项卡中。 给定目录中的文件数据源在 "**文件 DSN** " 选项卡中列出;在 "**文件 DSN** " 选项卡的 "**查找范围**" 框中输入要显示的目录。  
  
> [!NOTE]  
>  若要管理连接到64位平台下的32位驱动程序的数据源，请使用 c:\windows\sysWOW64\odbcad32.exe。 若要管理连接到64位驱动程序的数据源，请使用 c:\windows\system32\odbcad32.exe。 在64位 Windows 8 操作系统上的 "**管理工具**" 中，"32 位和64位**ODBC 数据源管理器**" 对话框中都有一些图标。  
  
 如果使用64位 odbcad32.exe 来配置或删除连接到32位驱动程序的 DSN （例如，**驱动程序是否进行 Microsoft Access （\*.mdb））**，则会收到以下错误消息：  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 若要解决此错误，请使用32位 odbcad32.exe 配置或删除该 DSN。  
  
 数据源将特定 ODBC 驱动程序与要通过该驱动程序访问的数据相关联。 例如，可以创建一个数据源，以便使用 ODBC dBASE 驱动程序访问在硬盘或网络驱动器上的特定目录中找到的一个或多个 dBASE 文件。 使用 ODBC 数据源管理器，可以添加、修改和删除数据源，如下表所述。  
  
|操作|说明|  
|------------|-----------------|  
|添加数据源|可以添加多个数据源，每个数据源都可以使用该驱动程序将驱动程序与要访问的某些数据相关联。 为每个数据源指定一个唯一标识该数据源的名称。 例如，如果为一组包含客户信息的 dBASE 文件创建数据源，则可以将数据源命名为 "Customers"。 应用程序通常会显示数据源名称，以便用户从中进行选择。<br /><br /> 添加文件数据源与添加用户或系统数据源略有不同。 有关详细信息，请参阅 ODBC 数据源管理器帮助文件。|  
|修改数据源|根据你的要求，你可能会发现需要重新配置数据源。 可以通过单击 "任何驱动程序设置" 对话框中的 "**配置**" 来重置选项。|  
|删除数据源|选择数据源后，单击 "**删除**"。|  
  
 有关文件数据源的详细信息，请参阅[使用文件数据源进行连接或使用](../../odbc/reference/develop-app/connecting-using-file-data-sources.md) [SQLDriverConnect 函数](../../odbc/reference/syntax/sqldriverconnect-function.md)连接。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC 数据源管理器](../../odbc/admin/odbc-data-source-administrator.md)
