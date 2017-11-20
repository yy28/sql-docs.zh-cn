---
title: "配置 Oracle ODBC 驱动程序 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- configuring ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], configuring
ms.assetid: 0a5f827c-0b80-4627-85cb-f10292b9fb33
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 64e6dfe9f31eb983170f08e9fcd3e0705ba9ae62
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="configuring-the-odbc-driver-for-oracle"></a>配置 Oracle ODBC 驱动程序
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 你可以通过知道数据环境并正确设置的参数的数据源连接通过控制适用于 Oracle 的 ODBC 驱动程序的性能[ODBC 数据源管理器](../../odbc/admin/odbc-data-source-administrator.md)对话框框中，或通过连接字符串参数。 对话框中提供了下列控件，用于连接到使用对话框中的数据源或使用连接字符串：  
  
-   **用户 DSN 选项卡**列出的计算机本地数据源名称。  
  
-   **系统 DSN 选项卡**使您能够添加或删除系统数据源。 可以通过在本地计算机上的所有用户访问系统数据源。  
  
-   **文件 DSN 选项卡**使您能够添加或删除从本地计算机文件数据源。 可由具有相同的驱动程序安装的所有用户共享文件数据源。  
  
-   **驱动程序选项卡**列出已安装的 ODBC 驱动程序。  
  
-   **跟踪选项卡**使您能够指定 ODBC 驱动程序管理器如何跟踪对 ODBC 函数的调用。 你可以配置为每个已安装的 ODBC 应用程序的单独的跟踪。  
  
-   **连接池选项卡**使您能够选择每个已安装的驱动程序的连接选项。  
  
-   **有关选项卡**列出已安装的 ODBC 组件文件。  
  
 添加数据源后，你可以使用**ODBC 数据源管理器**对话框可以配置对您的数据源的访问权限。 选择数据源，，然后单击一个选项卡以编辑或查看的信息。

