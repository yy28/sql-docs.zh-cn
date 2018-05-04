---
title: 连接到 Azure SQL DB (AccessToSQL) |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Connect to SQL Azure dialog box
ms.assetid: bf44b236-d9be-41ae-a5fd-bd73038e505f
caps.latest.revision: 17
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b23de92a365404164109b264a8e2c8d940190c5a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="connect-to-azure-sql-db-accesstosql"></a>连接到 Azure SQL DB (AccessToSQL)
用于连接到 SQL Azure 对话框连接到你想要迁移的 SQL Azure 数据库。  
  
若要访问此对话框中，在**文件**菜单上，选择**连接到 SQL Azure**。 如果你以前连接，则命令是**重新连接到 SQL Azure。**  
  
## <a name="options"></a>选项  
**服务器名称**  
  
选择或输入用于连接到 SQL Azure 服务器名称。  
  
**数据库**  
  
选择中，输入或**浏览**数据库名称。  
  
> [!IMPORTANT]  
> 在 SQL Azure 中访问的 SSMA 不支持对 master 数据库的连接。  
  
**用户名**  
  
输入 SSMA 将用于连接到 SQL Azure 数据库的用户名称  
  
**密码**  
  
输入用户名的密码。  
  
**Encrypt**  
  
SSMA 建议加密的连接到 SQL Azure。  
  
## <a name="create-azure-database"></a>创建 Azure 数据库  
若要创建新的 azure 数据库，请执行以下步骤  
  
1.  单击位于在连接到 SQL Azure 对话框中的浏览按钮  
  
2.  如果没有数据库，会出现两个菜单项  
  
    1.  **（未找到数据库）**这将禁用且灰出所有的时间  
  
    2.  **创建新的数据库**其始终处于启用状态，使用户可以在 SQL Azure 帐户上创建新的 azure 数据库。 单击此菜单项，在创建 azure 数据库对话框中是否存在与数据库名称和大小。  
  
3.  在创建数据库时，这两个参数作为输入提供。  
  
    1.  **数据库名称：**输入数据库名称。  
  
    2.  **数据库大小：**选择你需要在 SQL Azure 帐户中创建的数据库大小。  
  
