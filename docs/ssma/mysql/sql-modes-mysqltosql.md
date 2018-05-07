---
title: SQL 模式 (MySQLToSQL) |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: d840ee51-b863-4e77-84aa-37d3f094bfed
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 748348f5f9d2f97d359e585c77646bf5f5fd9ffa
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sql-modes-mysqltosql"></a>SQL 模式 (MySQLToSQL)
SSMA for MySQL 可以在不同的 SQL 模式下运行和可以适用于这些模式以不同的方式不同的客户端。  
  
模式定义应该支持 MySQL，SQL 语法和类型的数据验证检查它应执行。 这使得更轻松地在不同环境中使用 MySQL 并与 SQL Server 一起使用 MySQL。  
  
## <a name="sql-modes-grid"></a>SQL 模式网格：  
  
-   在根级别的 SQL 模式网格包含以下列： **SQL 模式名称**，**加载 SQL 模式**，和**有效 SQL 模式**。  
  
-   在数据库类别、 数据库、 表类别、 语句类别、 视图类别、 表、 视图、 函数、 过程、 UDF 和事件对象级别的 SQL 模式网格包含以下列： **SQL 模式名称**，**继承 SQL 模式**，和**有效 SQL 模式**。  
  
-   在存储过程、 存储函数和触发器级别的 SQL 模式网格包含以下列： **SQL 模式名称**，**原始 SQL 模式**，和**有效 SQL 模式**。  
  
> [!NOTE]  
> 组模式将显示在设置为粗体，列在 SQL 模式 Name。  
  
## <a name="loaded-sql-modes"></a>加载的 SQL 模式  
这些是 SQL 模式，但在会话或根级别设置。 无法编辑或修改一次加载到目标数据库 SQL 模式。  
  
## <a name="inherited-sql-modes"></a>继承的 SQL 模式  
这些是 SQL 模式，但从相应的父节点继承。  
  
除函数类别、 过程类别、 事件类别和触发器中，这些 SQL 模式可以在所有级别 （数据库、 表类别、 语句类别、 视图类别、 表、 视图、 函数、 过程、 UDF 和事件的对象） 都存在。  
  
> [!NOTE]  
> 通过选择**从父级继承**复选框，继承 SQL 模式可以从父节点继承。 默认情况下，此复选框处于选定状态。  
  
## <a name="original-sql-modes"></a>原始 SQL 模式  
这些是仅函数、 过程和触发器的级别上存在 SQL 模式。  
  
> [!NOTE]  
> 通过选择**使用原始**检查框中，最初在相应的函数中使用 SQL 模式或可以使用过程或触发器。 默认情况下，此复选框处于选定状态。  
  
## <a name="effective-sql-modes"></a>有效的 SQL 模式  
按以下方式，可以在各种级别定义有效的 SQL 模式：  
  
-   **在会话级别：**  
  
    1.  所有加载 SQL 模式可以调用，"有效 SQL 模式"。  
  
    2.  在此级别的有效 SQL 模式可以直接或显式修改。  
  
    3.  显式设置的有效 SQL 模式将不反映作为加载 SQL 模式，并且最后应用于对象。  
  
-   **在函数或过程或触发器级别：**  
  
    1.  所有原始 SQL 模式可以调用，"有效 SQL 模式"。  
  
    2.  在此级别，有效的 SQL 模式可以显式修改时，才**使用原始**复选框处于未选中状态。  
  
    3.  显式设置的有效 SQL 模式将不反映与原始 SQL 模式，并且最后应用于对象。  
  
-   **在函数或过程或触发器级别以外的节点：**  
  
    1.  所有继承 SQL 模式可以调用，"有效 SQL 模式"。  
  
    2.  在此级别，有效的 SQL 模式可以显式修改时，才**从父级继承**复选框处于未选中状态。  
  
    3.  显式设置的有效 SQL 模式将不反映与继承 SQL 模式，并且最后应用于对象。  
  
