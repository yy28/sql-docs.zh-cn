---
title: 数据源向导屏幕 1 (SQL Server 的 ODBC 驱动程序) |Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f6edf465f5b853008c9bdc8c420f6e862e360593
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936605"
---
# <a name="data-source-wizard-screen-1"></a>数据源向导屏幕 1

指定数据源的名称和说明，以及该数据源要连接的运行 SQL Server 的服务器名称。 
    
## <a name="options"></a>选项

### <a name="name"></a>“属性”

ODBC 应用程序请求与数据源连接时使用的数据源名称。 例如，“Personnel”。 该数据源名称显示在“ODBC 数据源管理器”对话框中。

### <a name="description"></a>描述

（可选）数据源的说明。 例如，“所有雇员的雇佣日期、发薪记录和当前审核”。

### <a name="select-or-enter-a-server-name"></a>选择或输入服务器名称

网络上 SQL Server 的实例名称。 您需要在下一个编辑框中指定一个服务器。

大多数情况下，ODBC 驱动程序可通过使用此框中提供的默认协议顺序和服务器名称进行连接。 如果要创建服务器别名或配置客户端网络库，请使用 SQL Server 配置管理器。

当使用与 SQL Server 相同的计算机时，你可以在服务器框中输入“(local)”。 即使正在运行非联网版的 SQL Server，用户也可以连接到 SQL Server 的本地实例。 在同一台计算机上可以运行 SQL Server 的多个实例。 若要指定 SQL Server 的命名实例，则将服务器名称指定为 _ServerName_\\_InstanceName_。

有关不同网络类型的服务器名称的详细信息，请参阅“SQL Server 联机丛书”中的 SQL Server 安装文档。

### <a name="finish"></a>“完成”

如果此屏幕上指定的信息为连接到 SQL Server 所需的全部信息，则可以单击“完成”。  对于在向导的其他屏幕上指定的所有属性都使用默认值。

### <a name="next"></a>Next

若要进入向导的下一个屏幕, 请单击 "**下一步**"。

## <a name="next-steps"></a>后续步骤

[数据源向导屏幕 2](../../../connect/odbc/windows/dsn-wizard-2.md)
