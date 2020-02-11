---
title: 连接到 Azure SQL DB （SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 96538007-1099-40c8-9902-edd07c5620ee
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 68fbac69959d423477750a69bb6e5b06ab62af2b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083473"
---
# <a name="connect-to-azure-sql-db--sybasetosql"></a>连接到 Azure SQL DB (SybaseToSQL)
使用 "连接到 Azure SQL DB" 对话框连接到要迁移的 Azure SQL DB 数据库。  
  
若要访问此对话框，请在 "**文件**" 菜单上选择 "**连接到 Azure SQL DB**"。 如果你以前已连接，则该命令将**重新连接到 AZURE SQL DB。**  
  
## <a name="options"></a>选项  
**服务器名称**  
  
选择或输入用于连接到 Azure SQL 数据库的服务器名称。  
  
**Database**  
  
选择，输入或**浏览**数据库名称。  
  
> [!IMPORTANT]  
> 用于 Sybase 的 SSMA 不支持连接到 Azure SQL DB 中的 master 数据库。  
  
**用户名**  
  
输入 SSMA 将用于连接到 Azure SQL DB 数据库的用户名  
  
**权限**  
  
输入用户名的密码。  
  
**加密**  
  
SSMA 建议将加密连接到 Azure SQL DB。  
  
## <a name="create-azure-database"></a>创建 Azure 数据库  
如果 Azure SQL DB 帐户中没有数据库，则可以创建第一个数据库。  
  
若要首次创建新数据库，请执行以下步骤：  
  
1.  单击 "连接到 Azure SQL DB" 对话框中的 "浏览" 按钮  
  
2.  如果没有数据库，将显示以下两个菜单项。  
  
    1.  **（未找到数据库）** 已禁用并且始终灰显  
  
    2.  **创建新的数据库**，仅当 AZURE SQL DB 帐户上没有数据库时才启用此功能。 单击此菜单项时，将显示 "创建 Azure 数据库" 对话框，其中包含数据库名称和大小。  
  
3.  创建数据库时，会将以下两个参数指定为输入：  
  
    1.  **数据库名称：** 输入数据库名称。  
  
    2.  **数据库大小：** 选择需要在 Azure SQL DB 帐户中创建的数据库大小。  
  
