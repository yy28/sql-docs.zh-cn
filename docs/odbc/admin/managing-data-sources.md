---
title: 管理数据源 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5069ac9a5babc3071c52d73d5b56b21729a5d8a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307208"
---
# <a name="managing-data-sources"></a>管理数据源
从驱动程序的安装程序安装 ODBC 驱动程序后，可以为其定义一个或多个数据源。 数据源名称 （DSN） 应提供数据的唯一描述;例如，*工资或**应付帐款*。 为当前安装的所有驱动程序定义的用户和系统数据源列在**ODBC 数据源管理员**对话框**的用户 DSN**或**系统 DSN**选项卡中。 给定目录中的文件数据源列在文件 DSN 选项卡中;**在"文件 DSN"** 选项卡中列出该文件数据源。要显示的目录在 **"文件 DSN"** 选项卡中的"**查找"** 框中输入。  
  
> [!NOTE]  
>  要管理在 64 位平台下连接到 32 位驱动程序的数据源，请使用 c：_windows_sysWOW64_odbcad32.exe。 要管理连接到 64 位驱动程序的数据源，请使用 c：_windows_system32_odbcad32.exe。 在 64 位 Windows 8 操作系统上的**管理工具**中，有 32 位和 64 位**ODBC 数据源管理员**对话框的图标。  
  
 如果使用 64 位 odbcad32.exe 配置或删除连接到 32 位驱动程序的 DSN，例如，**驱动程序执行 Microsoft 访问 （.mdb），\*** 您将收到以下错误消息：  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 要解决此错误，请使用 32 位 odbcad32.exe 配置或删除 DSN。  
  
 数据源将特定的 ODBC 驱动程序与要通过该驱动程序访问的数据关联。 例如，您可以创建数据源以使用 ODBC dBASE 驱动程序访问硬盘或网络驱动器上特定目录中的一个或多个 dBASE 文件。 使用 ODBC 数据源管理员，您可以添加、修改和删除数据源，如下表所述。  
  
|操作|描述|  
|------------|-----------------|  
|添加数据源|可以添加多个数据源，每个数据源将驱动程序与要使用该驱动程序访问的某些数据相关联。 为每个数据源指定唯一标识该数据源的名称。 例如，如果为一组包含客户信息的 dBASE 文件创建数据源，则可以将数据源命名为"客户"。 应用程序通常显示数据源名称供用户选择。<br /><br /> 添加文件数据源与添加用户或系统数据源略有不同。 有关详细信息，请参阅 ODBC 数据源管理员帮助文件。|  
|修改数据源|根据您的要求，您可能会发现有必要重新配置数据源。 您可以通过单击任何驱动程序设置对话框中的 **"配置"** 来重置选项。|  
|删除数据源|选择数据源后单击 **"删除**"。|  
  
 有关文件数据源的详细信息，请参阅[使用文件数据源或](../../odbc/reference/develop-app/connecting-using-file-data-sources.md) [SQLDriverConnect 函数](../../odbc/reference/syntax/sqldriverconnect-function.md)进行连接。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC 数据源管理器](../../odbc/admin/odbc-data-source-administrator.md)
