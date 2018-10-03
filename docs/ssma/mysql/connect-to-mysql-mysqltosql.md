---
title: 连接到 MySQL (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 94099d01-ab19-4d58-a172-340c86b4a0f3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2a68b60a954e6cd89698d4e906f8272f08d6b11e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47673155"
---
# <a name="connect-to-mysql-mysqltosql"></a>连接到 MySQL (MySQLToSQL)
使用**连接到 MySQL**对话框以连接到你想要迁移的 MySQL 数据库。  
  
若要访问此对话框，请在**文件**菜单中，选择**连接到 MySQL**。 如果你之前已连接，则命令是**重新连接到 MySQL**。  
  
## <a name="options"></a>选项  
**提供程序**  
  
可用的 MySQL 提供程序是 MySQL ODBC 5.1 驱动程序 （受信任）。  
  
**模式**  
  
默认模式为标准模式。 在标准模式下输入或选择 MySQL、 服务器名称、 服务器端口、 用户名称和密码的值。  
  
**服务器名称**  
  
输入 MySQL 服务器名称。 这是标准模式选项。  
  
**服务器端口**  
  
输入服务器端口。 默认服务器端口为 3306。 这是标准模式选项。  
  
**用户名**  
  
输入 SSMA 将用于连接到 MySQL 数据库的用户名。  
  
**密码**  
  
输入用户名的密码。  
  
**SSL**  
  
如果你想要安全地连接到 MySQL，请使用安全套接字层 (SSL) 通过检查**SSL**复选框。  
  
**配置**  
  
它提供了一个选项以配置 MySQL 通过安全套接字层 (SSL) 连接。  
  
> [!NOTE]  
> 若要启用**配置**，SSL 必须设置为**True**。  
  
在单击"配置"按钮，会出现一个对话框。 若要使用加密，而连接到 MySQL 数据库，以下三个证书中的文件的对话框中的路径必须被定义 [隐私增强邮件证书 (PEM)]:  
  
-   **SSL 证书颁发机构：** 信任 SSL Ca 的一系列指定文件的路径。  
  
-   **SSL 证书：** 指定要用于建立安全连接的 SSL 证书文件的名称。  
  
-   **SSL 密钥：** 指定要用于建立安全连接的 SSL 密钥文件的名称。  
  
> [!NOTE]  
> -   **确定**按钮已启用时提供了所需的信息。 如果任何文件路径无效，"确定"按钮将保持禁用状态。  
> -   **取消**按钮关闭对话框和**将关闭**主连接窗体中的 SSL 选项。  
  
