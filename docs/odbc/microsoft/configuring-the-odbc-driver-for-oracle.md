---
title: 配置 Oracle 的 ODBC 驱动程序 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1bbdbe36ed9e6f254e2b738479698bd9eece09f8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281367"
---
# <a name="configuring-the-odbc-driver-for-oracle"></a>配置 Oracle ODBC 驱动程序
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 您可以通过了解数据环境并通过[ODBC 数据源管理员](../../odbc/admin/odbc-data-source-administrator.md)对话框或通过连接字符串参数正确设置数据源连接的参数来控制 Oracle 的 ODBC 驱动程序的性能。 该对话框提供以下控件，用于使用对话框或使用连接字符串连接到数据源：  
  
-   **用户 DSN 选项卡**列出计算机本地的数据源名称。  
  
-   **系统 DSN 选项卡**使您能够添加或删除系统数据源。 本地计算机上的所有用户都可以访问系统数据源。  
  
-   **文件 DSN 选项卡**使您能够从本地计算机添加或删除文件数据源。 文件数据源可以由安装了相同驱动程序的所有用户共享。  
  
-   **驱动程序选项卡**列出已安装的 ODBC 驱动程序。  
  
-   **跟踪选项卡**使您能够指定 ODBC 驱动程序管理器跟踪对 ODBC 的调用功能。 您可以为每个已安装的 ODBC 应用程序单独配置跟踪。  
  
-   **连接池选项卡**使您能够为每个已安装的驱动程序选择连接选项。  
  
-   **关于选项卡**列出已安装的 ODBC 组件文件。  
  
 添加数据源后，可以使用**ODBC 数据源管理员**对话框配置对数据源的访问。 选择数据源，然后单击其中一个选项卡以编辑或查看信息。
