---
title: 通过笔记本部署 Azure SQL 数据库
description: 本教程介绍如何创建 Azure SQL 数据库。
author: ninarn
ms.author: ninarn
ms.reviewer: alayu, maghan
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: 88bb9fd980da21b20f0faf6f699147d26abe65b9
ms.sourcegitcommit: 76ab3b57718341c6057613c9bd38cf82fb17786e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2020
ms.locfileid: "92060854"
---
# <a name="create-an-azure-sql-database-using-azure-data-studio"></a>使用 Azure Data Studio 创建 Azure SQL 数据库

可以使用 Azure Data Studio 通过部署向导和笔记本创建 Azure SQL 数据库。

## <a name="pre-requisites"></a>先决条件

 - 已安装 [Azure Data Studio](download-azure-data-studio.md)
 - 有效的 Azure 帐户和订阅。 如果没有帐户，请[创建一个免费帐户](https://azure.microsoft.com/free/)。

## <a name="use-the-deployment-wizard"></a>使用部署向导

按照以下步骤使用部署向导，它将指导你在简单的 UI 体验中完成所需设置。

首先，在部署向导中找到并选择“Azure SQL 数据库”。

 1. 在 Azure Data Studio 中，在左侧导航栏中选择“连接 Viewlet”。
 2. 选择“连接”面板顶部的“...”按钮，然后选择“新建部署...” 
 3. 在部署向导中，选择“Azure SQL 数据库”磁贴，并选中“接受条款”复选框
 4. 在“资源类型”下拉列表中，选择要创建的内容（数据库、数据库服务器或弹性池）。 如果 Azure 中没有任何 SQL 数据库，我们建议首先创建一个数据库。
 5. 选择“在 Azure 门户中创建”

接下来，输入用于创建数据库、服务器或池的所有首选设置。 你可以在 [Azure SQL 文档](https://docs.microsoft.com/azure/azure-sql/database/single-database-create-quickstart?tabs=azure-portal)中找到有关如何配置这些设置的一些指导。

## <a name="next-steps"></a>后续步骤

创建数据库、服务器或池后，可以在 Azure Data Studio 中[连接和查询](quickstart-sql-database.md)数据库。
