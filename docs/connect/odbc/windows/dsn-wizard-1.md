---
title: "数据源向导屏幕 1 (ODBC Driver for SQL Server) |Microsoft 文档"
ms.custom: 
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 83474fa2c3acef62e015c62abff7ed17445a0389
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="data-source-wizard-screen-1"></a>数据源向导屏幕 1

指定的名称和说明的数据源，以及运行数据源将连接到的 SQL Server 的服务器的名称。 
    
## <a name="options"></a>选项

### <a name="name"></a>Name

ODBC 应用程序请求与数据源连接时使用的数据源名称。 例如，“Personnel”。 该数据源名称显示在“ODBC 数据源管理器”对话框中。

### <a name="description"></a>Description

（可选）数据源的说明。 例如，“所有雇员的雇佣日期、发薪记录和当前审核”。

### <a name="select-or-enter-a-server-name"></a>选择或输入服务器名称

你的网络上的 SQL Server 实例的名称。 您需要在下一个编辑框中指定一个服务器。

在大多数情况下，可以通过使用默认协议顺序以及在此框中提供的服务器名称连接的 ODBC 驱动程序。 如果你想要创建服务器的别名或配置客户端网络库，请使用 SQL Server 配置管理器。

你可以输入"(local)"在服务器中时要用作 SQL Server 在同一台计算机。 然后，用户可以连接到 SQL Server，即使当运行非联网版本的 SQL Server 的本地实例。 多个 SQL Server 实例可以在同一台计算机上运行。 若要指定 SQL Server 的命名的实例，服务器名称指定为_ServerName_\\_InstanceName_。

有关不同类型的网络的服务器名称的详细信息，请参阅 SQL Server 联机丛书中的 SQL Server 安装文档。

### <a name="finish"></a>完成

如果在此屏幕上指定的信息为所有所需连接到 SQL Server，你可以单击**完成**。 对于在向导的其他屏幕上指定的所有属性都使用默认值。

### <a name="next"></a>Next

若要转到向导的下一个屏幕，请单击**下一步**。

## <a name="next-steps"></a>后续步骤

[数据源向导屏幕 2](../../../connect/odbc/windows/dsn-wizard-2.md)
