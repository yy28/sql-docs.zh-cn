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
ms.openlocfilehash: bc163f53c9dc234702f6f74426eb65f57cec26b5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096677"
---
# <a name="configuring-the-odbc-driver-for-oracle"></a>配置 Oracle ODBC 驱动程序
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 通过了解数据环境，并通过 " [ODBC 数据源管理器](../../odbc/admin/odbc-data-source-administrator.md)" 对话框或通过连接字符串参数正确设置数据源连接的参数，可以控制用于 ORACLE 的 ODBC 驱动程序的性能。 此对话框提供以下控件，用于通过对话框或使用连接字符串连接到数据源：  
  
-   **用户 DSN 选项卡**列出计算机本地的数据源名称。  
  
-   **系统 DSN 选项卡**允许您添加或删除系统数据源。 本地计算机上的所有用户都可以访问系统数据源。  
  
-   **文件 DSN 选项卡**允许您在本地计算机上添加或删除文件数据源。 安装了相同驱动程序的所有用户都可以共享文件数据源。  
  
-   **驱动程序选项卡**列出已安装的 ODBC 驱动程序。  
  
-   **跟踪选项卡**使您能够指定 ODBC 驱动程序管理器跟踪对 ODBC 函数的调用的方式。 可以为每个已安装的 ODBC 应用程序单独配置跟踪。  
  
-   **"连接池" 选项卡**使你能够为每个已安装的驱动程序选择连接选项。  
  
-   **关于选项卡**列出已安装的 ODBC 组件文件。  
  
 添加数据源后，可以使用 " **ODBC 数据源管理器**" 对话框来配置对数据源的访问。 选择一个数据源，然后单击其中一个选项卡以编辑或查看信息。
