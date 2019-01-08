---
title: SQL 模式 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: d840ee51-b863-4e77-84aa-37d3f094bfed
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6965d67b6dae484b3fa72f215446682f9aa6760c
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52394870"
---
# <a name="sql-modes-mysqltosql"></a>SQL 模式 (MySQLToSQL)
SSMA for MySQL 可以运行在不同的 SQL 模式，并可以应用这些模式以不同的方式为不同的客户端。  
  
模式定义应支持 MySQL、 SQL 语法和类型的数据验证检查应执行。 这使得更易于在不同的环境中使用 MySQL 和 SQL Server 使用 MySQL。  
  
## <a name="sql-modes-grid"></a>SQL 模式网格：  
  
-   根级别上的 SQL 模式网格包含以下列：**SQL 模式名称**，**加载 SQL 模式**，和**有效 SQL 模式**。  
  
-   在数据库类别、 数据库、 表类别、 语句类别、 视图类别、 表、 视图、 函数、 过程、 UDF 和事件对象级别的 SQL 模式网格包含以下列：**SQL 模式名称**，**继承 SQL 模式**，和**有效 SQL 模式**。  
  
-   在存储过程、 存储函数和触发器的级别的 SQL 模式网格包含以下列：**SQL 模式名称**，**原始 SQL 模式**，和**有效 SQL 模式**。  
  
> [!NOTE]  
> 组模式中将显示列下，粗体 SQL 模式 Name。  
  
## <a name="loaded-sql-modes"></a>加载的 SQL 模式  
这些是在会话或根级别上设置 SQL 模式。 无法编辑或修改一次加载到目标数据库在 SQL 模式。  
  
## <a name="inherited-sql-modes"></a>继承的 SQL 模式  
这些是 SQL 模式的继承自相应的父节点。  
  
除函数类别、 过程类别、 事件类别和触发器中，SQL，这些模式可以在所有级别 （数据库、 表类别、 语句类别、 视图类别、 表、 视图、 函数、 过程、 UDF 和事件对象） 上才存在。  
  
> [!NOTE]  
> 通过选择**从父级继承**复选框，继承 SQL 模式可以继承自父节点。 默认情况下，此复选框处于选定状态。  
  
## <a name="original-sql-modes"></a>原始 SQL 模式  
这些是仅函数、 过程和触发器的级别上存在 SQL 模式。  
  
> [!NOTE]  
> 通过选择**使用原始**复选框中，相应的函数中最初使用 SQL 模式或可以使用过程或触发器。 默认情况下，此复选框处于选定状态。  
  
## <a name="effective-sql-modes"></a>有效的 SQL 模式  
可以在不同级别定义有效的 SQL 模式，如下所示：  
  
-   **在会话级别：**  
  
    1.  所有加载 SQL 模式可以调用，"有效 SQL 模式"。  
  
    2.  在此级别，有效的 SQL 模式可以直接和显式修改。  
  
    3.  显式设置的有效 SQL 模式不反映为加载 SQL 模式以及最后应用于对象。  
  
-   **在函数或过程或触发器的级别：**  
  
    1.  所有原始 SQL 模式可以调用，"有效 SQL 模式"。  
  
    2.  在此级别，有效的 SQL 模式可以进行显式修改时，才**使用原始**复选框处于未选中状态。  
  
    3.  显式设置的有效 SQL 模式不反映作为原始 SQL 模式，并且最后应用于对象。  
  
-   **在函数或过程或触发器级别以外的节点：**  
  
    1.  所有继承 SQL 模式可以调用，"有效 SQL 模式"。  
  
    2.  在此级别，有效的 SQL 模式可以进行显式修改时，才**从父级继承**复选框处于未选中状态。  
  
    3.  显式设置的有效 SQL 模式不反映为继承 SQL 模式以及最后应用于对象。  
  
