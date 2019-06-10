---
title: 快速入门：连接和查询 PostgreSQL
titleSuffix: Azure Data Studio
description: 本快速入门介绍如何使用 Azure Data Studio 来连接到 PostgreSQL，并运行查询
ms.custom: seodec18
ms.date: 03/19/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: rachel-msft
ms.author: raagyema
manager: jroth
ms.openlocfilehash: be8683ae563e4e0676f53203cb40386cf8aa4840
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66778331"
---
# <a name="quickstart-connect-and-query-postgresql-using-includename-sosincludesname-sos-shortmd"></a>快速入门：连接和查询 PostgreSQL 使用 [!INCLUDE[name-sos](../includes/name-sos-short.md)]
本快速入门介绍如何使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]若要连接到 Postgres，以及如何将 SQL 语句来创建数据库*tutorialdb*和对其进行查询。

## <a name="prerequisites"></a>先决条件

若要完成本快速入门教程，需要[!INCLUDE[name-sos](../includes/name-sos-short.md)]，适用于的 PostgreSQL 扩展 [!INCLUDE[名称 sos](../includes/name-sos-short.md)，并且有权 PostgreSQL 服务器。

- [安装[!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md)。
- [安装适用于 Azure Data Studio PostgreSQL 扩展](postgres-extension.md)。
- [安装 PostgreSQL](https://www.postgresql.org/download/)。 (或者，可以创建一个 Postgres 数据库中云采用[向上 az postgres](https://docs.microsoft.com/azure/postgresql/quickstart-create-server-up-azure-cli))。 

## <a name="connect-to-postgresql"></a>连接到 PostgreSQL

1. 启动 **[!INCLUDE[name-sos](../includes/name-sos-short.md)]** 。

2. 首次启动[!INCLUDE[name-sos](../includes/name-sos-short.md)]**连接**对话框随即打开。 如果**连接**对话框未打开，请单击**服务器**页面中的**新的连接**图标：

   ![新的连接图标](media/quickstart-postgresql/new-connection-icon.png)

3. 在弹出表单中，转到**连接类型**，然后选择**PostgreSQL**从下拉列表。


4. 填写其余字段使用用于 PostgreSQL 服务器的服务器名称、 用户名和密码。 

   ![新连接屏幕](media/quickstart-postgresql/new-connection-screen.png)  

   | 设置       | 示例值 | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **服务器名称** | localhost | 完全限定的服务器名称 |
   | **用户名** | postgres | 你想要登录的用户名。 |
   | **密码（SQL 登录名）** | *password* | 中的登录帐户的密码。 |
   | **密码** | *检查* | 如果不想要连接的每次都输入密码，请选中此框。 |
   | **数据库名称** | \<默认\> | 如果你想要指定数据库的连接，请填写此。 |
   | **服务器组** | \<默认\> | 此选项可让你可以将此连接分配到特定服务器组中创建。 | 
   | **名称 （可选）** | *将保留为空* | 此选项可以指定你的服务器的友好名称。 | 

5. 选择“连接”  。 

在中打开你的服务器成功连接后，**服务器**侧栏。


## <a name="create-a-database"></a>创建数据库

以下步骤创建一个名为数据库**tutorialdb**:

1. 右键单击在 PostgreSQL 服务器**服务器**侧栏，然后选择**新查询**。

2. 在打开查询编辑器中粘贴此 SQL 语句。

   ```sql
   CREATE DATABASE tutorialdb;
   ```

3. 从工具栏中选择**运行**以执行查询。 通知出现在**消息**窗格来显示查询进度。

>[!TIP]
> 可以使用**F5**上执行语句，而不是使用你键盘**运行**。

在查询完成后，右键单击**数据库**，然后选择**刷新**以查看**tutorialdb**下的列表中**数据库**节点.


## <a name="create-a-table"></a>创建表

 以下步骤中创建表**tutorialdb**:

1. 更改到的连接上下文**tutorialdb**在查询编辑器中使用下拉列表。 

   ![更改上下文](media/quickstart-postgresql/change-context.png)

2. 以下 SQL 语句粘贴到查询编辑器，然后单击**运行**。 

   > [!NOTE]
   > 可以将其追加或覆盖在编辑器中的现有查询。 单击**运行**执行突出显示查询。 如果突出显示任何内容时，单击**运行**执行所有查询编辑器中。

   ```sql
   -- Drop the table if it already exists
   DROP TABLE IF EXISTS customers;
   -- Create a new table called 'customers'
   CREATE TABLE customers(
       customer_id SERIAL PRIMARY KEY,
       name VARCHAR (50) NOT NULL,
       location VARCHAR (50) NOT NULL,
       email VARCHAR (50) NOT NULL
   );
   ```

## <a name="insert-rows"></a>插入行

将以下代码段粘贴到查询窗口中，然后单击**运行**：

   ```sql
   -- Insert rows into table 'customers'
   INSERT INTO customers
       (customer_id, name, location, email)
    VALUES
      ( 1, 'Orlando', 'Australia', ''),
      ( 2, 'Keith', 'India', 'keith0@adventure-works.com'),
      ( 3, 'Donna', 'Germany', 'donna0@adventure-works.com'),
      ( 4, 'Janet', 'United States','janet1@adventure-works.com');
   ```

## <a name="query-the-data"></a>查询数据

1. 以下代码片段粘贴到查询编辑器，然后单击**运行**:
   
   ```sql
   -- Select rows from table 'customers'
   SELECT * FROM customers; 
   ```

2. 显示查询的结果：

   ![查看结果](media/quickstart-postgresql/view-results.png)

## <a name="next-steps"></a>后续步骤

了解如何[方案可用于在 Azure Data Studio Postgres](postgres-extension.md)。 