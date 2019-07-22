---
title: 如何：在脚本之间导航 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.editor.howto.navigate
ms.assetid: 8664bde5-86ff-4e8b-b5a6-af003316f6ad
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b5ff9e02b15c70d08151384bb46332e8b4ea550a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035166"
---
# <a name="how-to-navigate-between-scripts"></a>如何：在脚本之间导航
用于脱机部署的 Transact\-SQL 编辑器提供两种 Visual Studio 用户所熟悉的有用导航工具：“转到定义”和“查找所有引用”。 例如，您可以右键单击某个表名称，然后使用“查找所有引用”来列出项目中对该表的所有引用。 您可以双击某一搜索结果以转到特定的代码文件。 在此文件中，您可以再次右键单击表名称，然后选择“转到定义”以返回到表定义。  
  
> [!WARNING]  
> 以下过程利用在[连接的数据库开发](../ssdt/connected-database-development.md)和[面向项目的脱机数据库开发](../ssdt/project-oriented-offline-database-development.md)部分中的之前过程中创建的实体。  
  
### <a name="to-navigate-between-scripts"></a>在脚本之间导航  
  
1.  在“解决方案资源管理器”中展开“函数”文件夹，然后双击“GetProductsBySupplier.sql”。  
  
2.  在此行代码中右键单击 `Products`，然后选择“转到定义”  
  
    ```  
    SELECT * from Products p  
    ```  
  
3.  Products.sql 将自动打开，并且显示定义 `Products` 类型的位置。  
  
4.  返回到 GetProductsBySupplier.sql。 这次在 `Products` 的上下文菜单中选择“查找所有引用”。 在“查找符号结果”窗格中，你将看到引用了 `Products` 表的位置的列表。 双击任何搜索结果将转到该引用的位置。  
  
