---
title: 连接到 Azure SQL DB (AccessToSQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 57a745385de80a3040897310ddc5b43b1301ea86
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47717475"
---
# <a name="connect-to-azure-sql-db-accesstosql"></a>连接到 Azure SQL DB (AccessToSQL)
用于连接到 SQL Azure 对话框的连接到你想要迁移的 SQL Azure 数据库。  
  
若要访问此对话框，请在**文件**菜单中，选择**连接到 SQL Azure**。 如果你之前已连接，则命令是**重新连接到 SQL Azure。**  
  
## <a name="options"></a>选项  
**服务器名称**  
  
选择或输入用于连接到 SQL Azure 服务器名称。  
  
**“数据库”**  
  
选择中，输入或**浏览**数据库名称。  
  
> [!IMPORTANT]  
> 适用于 Access 的 SSMA 不支持在 SQL Azure 中的对 master 数据库的连接。  
  
**用户名**  
  
输入 SSMA 将用于连接到 SQL Azure 数据库的用户名称  
  
**密码**  
  
输入用户名的密码。  
  
**Encrypt**  
  
SSMA 建议加密的连接到 SQL Azure。  
  
## <a name="create-azure-database"></a>创建 Azure 数据库  
若要创建新的 azure 数据库，请执行以下步骤  
  
1.  单击浏览按钮显示在连接到 SQL Azure 对话框的  
  
2.  如果不存在数据库，两个菜单项显示  
  
    1.  **（找不到数据库）** 的已禁用，所有时间会变灰  
  
    2.  **创建新的数据库**始终启用的使用户可以在 SQL Azure 帐户上创建新的 azure 数据库。 单击此菜单项，创建 azure 数据库对话框是包含数据库名称和大小。  
  
3.  在创建数据库时，这两个参数是作为输入提供。  
  
    1.  **数据库名称：** 输入数据库名称。  
  
    2.  **数据库大小：** 选择您需要在 SQL Azure 帐户中创建的数据库大小。  
  
