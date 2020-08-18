---
description: '连接到 Azure SQL 数据库 (SybaseToSQL) '
title: " (SybaseToSQL) 连接到 Azure SQL 数据库 |Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 96538007-1099-40c8-9902-edd07c5620ee
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 3717cce895ca602a550d47ea5c569af4c80963a0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492310"
---
# <a name="connect-to-azure-sql-database--sybasetosql"></a>连接到 Azure SQL 数据库 (SybaseToSQL) 
使用 "连接到 Azure SQL 数据库" 对话框连接到要迁移的 Azure SQL 数据库数据库。  
  
若要访问此对话框，请在 " **文件** " 菜单上选择 " **连接到 Azure SQL 数据库**"。 如果你以前已连接，则该命令将 **重新连接到 AZURE SQL 数据库。**  
  
## <a name="options"></a>选项  
**服务器名称**  
  
选择或输入用于连接到 Azure SQL 数据库的服务器名称。  
  
**Database**  
  
选择，输入或 **浏览** 数据库名称。  
  
> [!IMPORTANT]  
> 用于 Sybase 的 SSMA 不支持连接到 Azure SQL 数据库中的 master 数据库。  
  
**用户名**  
  
输入 SSMA 将用于连接到 Azure SQL 数据库数据库的用户名  
  
**密码**  
  
输入用户名的密码。  
  
**Encrypt**  
  
SSMA 建议对 Azure SQL 数据库进行加密连接。  
  
## <a name="create-azure-database"></a>创建 Azure 数据库  
如果 Azure SQL 数据库帐户中没有数据库，则可以创建第一个数据库。  
  
若要首次创建新数据库，请执行以下步骤：  
  
1.  单击 "连接到 Azure SQL 数据库" 对话框中的 "浏览" 按钮  
  
2.  如果没有数据库，将显示以下两个菜单项。  
  
    1.  ** (找不到任何数据库) 该数据库 ** 处于禁用状态并始终灰显  
  
    2.  **创建新的数据库** ，仅当 Azure SQL 数据库帐户上没有数据库时才启用此功能。 单击此菜单项时，将显示 "创建 Azure 数据库" 对话框，其中包含数据库名称和大小。  
  
3.  创建数据库时，会将以下两个参数指定为输入：  
  
    1.  **数据库名称：** 输入数据库名称。  
  
    2.  **数据库大小：** 选择需要在 Azure SQL 数据库帐户中创建的数据库大小。  
  
