---
title: 连接到 Azure SQL DB （AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connect to SQL Azure dialog box
ms.assetid: bf44b236-d9be-41ae-a5fd-bd73038e505f
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 0b26ddaef1373544e0df2fd9186cdf56fdafd801
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68040627"
---
# <a name="connect-to-azure-sql-db-accesstosql"></a>连接到 Azure SQL DB （AccessToSQL）
使用 "连接到 SQL Azure" 对话框连接到要迁移的 SQL Azure 数据库。  
  
若要访问此对话框，请在 "**文件**" 菜单上，选择 "**连接到 SQL Azure**"。 如果以前已连接，则该命令将**重新连接到 SQL Azure。**  
  
## <a name="options"></a>选项  
**服务器名称**  
  
选择或输入用于连接到 SQL Azure 的服务器名称。  
  
**Database**  
  
选择，输入或**浏览**数据库名称。  
  
> [!IMPORTANT]  
> SSMA for Access 不支持连接到 SQL Azure 中的 master 数据库。  
  
**用户名**  
  
输入 SSMA 将用于连接 SQL Azure 数据库的用户名  
  
**权限**  
  
输入用户名的密码。  
  
**加密**  
  
SSMA 建议将加密连接 SQL Azure。  
  
## <a name="create-azure-database"></a>创建 Azure 数据库  
若要创建新的 azure 数据库，请按照以下步骤操作  
  
1.  单击 "连接到 SQL Azure" 对话框中的 "浏览" 按钮  
  
2.  如果没有数据库，则显示两个菜单项  
  
    1.  **（未找到数据库）** 已禁用并且始终灰显  
  
    2.  创建始终启用的**新数据库**，使用户能够在 SQL Azure 帐户上创建新的 azure 数据库。 单击此菜单项时，将显示 "创建 azure 数据库" 对话框，其中包含数据库名称和大小。  
  
3.  创建数据库时，会将这两个参数指定为输入。  
  
    1.  **数据库名称：** 输入数据库名称。  
  
    2.  **数据库大小：** 选择需要在 SQL Azure 帐户中创建的数据库大小。  
  
