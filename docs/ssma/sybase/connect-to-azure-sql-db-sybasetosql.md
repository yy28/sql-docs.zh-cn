---
title: 连接到 Azure SQL DB (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 96538007-1099-40c8-9902-edd07c5620ee
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 057a39fd393be6cce9232d787b0d110a4be2035a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47640900"
---
# <a name="connect-to-azure-sql-db--sybasetosql"></a>连接到 Azure SQL DB (SybaseToSQL)
用于连接到 Azure SQL 数据库对话框的连接到你想要迁移的 Azure SQL DB 数据库。  
  
若要访问此对话框，请在**文件**菜单中，选择**连接到 Azure SQL DB**。 如果你之前已连接，则命令是**重新连接到 Azure SQL DB。**  
  
## <a name="options"></a>选项  
**服务器名称**  
  
选择或输入用于连接到 Azure SQL DB 服务器名称。  
  
**“数据库”**  
  
选择中，输入或**浏览**数据库名称。  
  
> [!IMPORTANT]  
> 适用于 Sybase 的 SSMA 不支持在 Azure SQL DB 中的对 master 数据库的连接。  
  
**用户名**  
  
输入 SSMA 将用于连接到 Azure SQL DB 数据库的用户名称  
  
**密码**  
  
输入用户名的密码。  
  
**Encrypt**  
  
SSMA 建议加密的连接到 Azure SQL DB。  
  
## <a name="create-azure-database"></a>创建 Azure 数据库  
如果在 Azure SQL DB 帐户中不存在数据库，可以创建第一个数据库。  
  
若要为第一次创建新的数据库，请执行以下步骤  
  
1.  单击浏览按钮显示在连接到 Azure SQL 数据库对话框的  
  
2.  如果不不存在任何数据库，将显示以下两个菜单项。  
  
    1.  **（找不到数据库）** 的已禁用，所有时间会变灰  
  
    2.  **创建新的数据库**仅当 Azure SQL 数据库帐户上没有任何数据库时启用的。 单击此菜单项，对话框中创建 Azure 数据库不存在具有数据库名称和大小。  
  
3.  在创建数据库时，作为输入提供以下两个参数：  
  
    1.  **数据库名称：** 输入数据库名称。  
  
    2.  **数据库大小：** 选择您需要在 Azure SQL DB 帐户中创建的数据库大小。  
  
