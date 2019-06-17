---
title: 配置用于 Oracle 的 ODBC 驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- configuring ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], configuring
ms.assetid: 0a5f827c-0b80-4627-85cb-f10292b9fb33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae444cfb293e12bd94281957335da1d4f4a97885
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63301753"
---
# <a name="configuring-the-odbc-driver-for-oracle"></a>配置 Oracle ODBC 驱动程序
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 可以通过了解数据环境并且正确地设置数据源连接通过参数来控制用于 Oracle 的 ODBC 驱动程序的性能[ODBC 数据源管理器](../../odbc/admin/odbc-data-source-administrator.md)对话框框中或通过连接字符串参数。 对话框中提供以下控件，用于连接到使用对话框中的数据源或使用连接字符串：  
  
-   **用户 DSN 选项卡**列出计算机本地的数据源名称。  
  
-   **系统 DSN 选项卡**，可添加或删除系统数据源。 可以通过在本地计算机上的所有用户访问系统数据源。  
  
-   **文件 DSN 选项卡**，可添加或从本地计算机中删除文件数据源。 可由具有相同的驱动程序安装的所有用户共享文件数据源。  
  
-   **驱动程序选项卡**列出已安装的 ODBC 驱动程序。  
  
-   **跟踪选项卡**使您能够指定 ODBC 驱动程序管理器如何跟踪对 ODBC 函数的调用。 你可以配置为每个已安装的 ODBC 应用程序单独跟踪。  
  
-   **连接池选项卡**使您能够选择每个已安装的驱动程序的连接选项。  
  
-   **有关选项卡**列出已安装的 ODBC 组件文件。  
  
 添加数据源后，可以使用**ODBC 数据源管理器**对话框可以配置对您的数据源的访问权限。 选择数据源，并单击其中一个选项卡来编辑或查看的信息。
