---
title: "hierarchyid (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- hierarchyid
- hierarchyid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Hierarchy data type
- hierarchyid data type
ms.assetid: 69b756e0-a1df-45b3-8a24-6ded8658aefe
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 44299e7ddb90bdd52e2638dd859993513bd6f966
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="hierarchyid-data-type-method-reference"></a>hierarchyid 数据类型方法引用
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

**Hierarchyid**数据类型是长度可变，系统数据类型。 使用**hierarchyid**来表示层次结构中的位置。 类型为 **hierarchyid** 的列不会自动表示树。 由应用程序来生成和分配 **hierarchyid** 值，使行与行之间的所需关系反映在这些值中。
  
**hierarchyid** 数据类型的值表示树层次结构中的位置。 **hierarchyid** 的值具有以下属性：
  
-   非常紧凑  
     在具有 *n* 个节点的树中，表示一个节点所需的平均位数取决于平均端数（节点的平均子级数）。 端数较小时 (0-7)，大小约为 6\*logA *n* 位，其中 A 是平均端数。 对于平均端数为 6 级、包含 100,000 个人的组织层次结构，一个节点大约占 38 位。 存储时，此值向上舍入为 40 位，即 5 字节。  
-   按深度优先顺序进行比较  
     给定两个 **hierarchyid** 值 **a** 和 **b**，**a<b** 表示在对树进行深度优先遍历时，先找到 a，后找到 b。 **hierarchyid** 数据类型的索引按深度优先顺序排序，在深度优先遍历中相邻的节点的存储位置也相邻。 例如，一条记录的子级的存储位置与该记录的存储位置是相邻的。 有关详细信息，请参阅[层次结构数据 &#40;SQL server&#41;](../../relational-databases/hierarchical-data-sql-server.md).  
-   支持任意插入和删除  
     使用 [GetDescendant](../../t-sql/data-types/getdescendant-database-engine.md) 方法，始终可以在任意给定节点的右侧、左侧或任意两个同级节点之间生成同级节点。 在层次结构中插入或删除任意数目的节点时，该比较属性保持不变。 大多数插入和删除操作都保留了紧凑性属性。 但是，对于在两个节点之间执行的插入操作，所产生的 hierarchyid 值的表示形式在紧凑性方面将稍微降低。  
-   在中使用的编码**hierarchyid**类型仅限于 892 字节。 因此，具有在其表示形式，使其适合 892 字节太多级别的节点不能表示**hierarchyid**类型。  
  
**Hierarchyid**类型可供作为 CLR 客户端**SqlHierarchyId**数据类型。
  
## <a name="remarks"></a>注释  
**Hierarchyid**类型以逻辑方式将层次结构树中的单个节点有关的信息编码进行编码到节点从树的根路径。 这种路径在逻辑上表示为一个在根之后被访问的所有子级的节点标签序列。 表示形式以一条斜杠开头，只访问根的路径由单条斜杠表示。 对于根以下的各级，各标签编码为由点分隔的整数序列。 子级之间的比较就是按字典顺序比较由点分隔的整数序列。 每个级别后面紧跟着一个斜杠。 因此斜杠将父级与其子级分隔开。 例如，下面是有效**hierarchyid**长度 1、 2、 2、 3 和 3 的路径分别级别：
  
-   /  
  
-   /1/  
  
-   /0.3.-7/  
  
-   /1/3/  
  
-   /0.1/0.2/  
  
可在任何位置插入节点。 节点之后插入**/1/2/**之前**/1/3/**可以表示为**/1/2.5/**。 插入在 0 之前的节点的逻辑表示形式为一个负数。 例如，之前的节点**/1/1/**可以表示为**/1/1 /**。 节点不能有前导零。 例如， **/1/1.1/**有效，但**/1/1.01/**无效。 若要防止出现错误，通过使用插入节点[GetDescendant](../../t-sql/data-types/getdescendant-database-engine.md)方法。
  
## <a name="data-type-conversion"></a>数据类型转换
**Hierarchyid**数据类型可以转换为其他数据类型，如下所示：
-   使用[tostring （)](../../t-sql/data-types/tostring-database-engine.md)方法将转换**hierarchyid**作为的逻辑表示形式的值**nvarchar （4000)**数据类型。  
-   使用[读取 （）](../../t-sql/data-types/read-database-engine.md)和[编写 （）](../../t-sql/data-types/write-database-engine.md)要转换**hierarchyid**到**varbinary**。  
-   传输**hierarchyid**参数通过 SOAP 首先将其强制转换为字符串。  
  
## <a name="upgrading-databases"></a>升级数据库
在数据库升级到[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，新的程序集和**hierarchyid**数据类型将自动安装。 升级顾问规则将检测具有冲突名称的任何用户类型或程序集。 升级顾问将建议重命名所有冲突程序集，并重命名所有冲突类型或在代码中用由两部分组成的名称来引用该预先存在的用户类型。
  
如果数据库升级检测到用户程序集具有冲突名称，它将自动重命名该程序集，并将数据库置于可疑模式下。
  
如果在升级过程中存在具有冲突名称的用户类型，则不会采取特殊步骤。 升级后，旧的用户类型和新的系统类型将同时存在。 用户类型将只能通过由两部分组成的名称使用。
  
## <a name="using-hierarchyid-columns-in-replicated-tables"></a>在复制的表中使用 hierarchyid 列
类型的列**hierarchyid**可以在任何复制的表上使用。 应用程序的要求取决于复制是单向的还是双向的，同时还取决于所用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本。
  
### <a name="one-directional-replication"></a>单向复制
单向复制包括快照复制、事务复制，以及在订阅服务器上不做更改的合并复制。 如何**hierachyid**列可以使用某个方向复制依赖的新版[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器正在运行。
-   A[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]发布服务器可以复制**hierachyid**列[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]而无需任何特殊注意事项的订阅服务器。  
-   A[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]发布服务器必须将转换**hierarchyid**列以将其复制到订阅服务器运行[!INCLUDE[ssEW](../../includes/ssew-md.md)]或早期版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssEW](../../includes/ssew-md.md)]和早期版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不支持**hierarchyid**列。 如果您使用的是这些版本之一，仍然可以将数据复制到订阅服务器。 为此，必须设置架构选项或发布兼容性级别（如果是合并复制），从而使列能够转换为兼容的数据类型。  
  
这两种情况均支持列筛选。 这包括过滤掉**hierarchyid**列。 只要筛选器不包括支持行筛选**hierarchyid**列。
  
### <a name="bi-directional-replication"></a>双向复制
双向复制包括带更新订阅的事务复制、对等事务复制，以及在订阅服务器上进行更改的合并复制。 复制允许你配置一个表，其中**hierarchyid**双向复制的列。 请注意以下要求和事项。
-   发布服务器和所有订阅服务器必须运行 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
-   复制将数据作为字节复制，且不会执行任何验证来确保层次结构的完整性。  
-   在源位置（订阅服务器或发布服务器）所做的更改复制到目标位置时，不保留其层次结构。  
-   哈希值**hierarchyid**列是特定于生成这些数据库。 因此，在发布服务器和订阅服务器上可以生成相同的值，但该值可以应用于不同的行。 复制不会检查此条件，并且没有分区到没有内置方法**hierarchyid**列值，因为没有为标识列。 应用程序必须使用约束或其他机制来避免这类未检测到的冲突。  
-   在订阅服务器上插入的行可能被孤立。 可能已在发布服务器上删除了所插入行的父行。 将订阅服务器上的行插入到发布服务器上时，这将导致出现未检测到的冲突。  
-   列筛选器无法筛选出不可为 null **hierarchyid**列： 来自订阅服务器上的 insert 语句将失败，因为没有默认值为**hierarchyid**发布服务器上的列。  
-   只要筛选器不包括支持行筛选**hierarchyid**列。  
  
## <a name="see-also"></a>另请参阅
[分层数据 (SQL Server)](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid 数据类型方法引用](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  

