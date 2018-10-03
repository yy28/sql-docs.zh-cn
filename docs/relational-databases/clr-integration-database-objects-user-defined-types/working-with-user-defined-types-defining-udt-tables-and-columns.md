---
title: 定义 UDT 表和列 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined types [CLR integration], columns
- UDTs [CLR integration], columns
- columns [CLR integration]
- user-defined types [CLR integration], tables
- tables [CLR integration]
- UDTs [CLR integration], tables
- UDTs [CLR integration], indexes
- user-defined types [CLR integration], indexes
- indexes [CLR integration]
ms.assetid: aea495f4-ce26-4952-b019-38f012625f3f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bf8c7dd55130026c54cc4e7b8aa24e1c99e96ada
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47855041"
---
# <a name="working-with-user-defined-types---defining-udt-tables-and-columns"></a>使用用户定义类型 - 定义 UDT 表和列
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  一旦包含用户定义类型 (UDT) 的程序集定义中注册了[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库，可在列定义。  
  
## <a name="creating-tables-with-udts"></a>使用 UDT 创建表  
 没有用于在表中创建 UDT 列的特殊语法。 您可以在某一列定义中使用 UDT 的名称，就像它是某一内部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型一样。 以下 CREATE TABLE[!INCLUDE[tsql](../../includes/tsql-md.md)]语句创建名为的表**点**，使用名为的列**ID**其定义为**int**标识列和表的的主键。 第二个列被命名为**PointValue**，使用的数据类型为**点**。 在此示例中使用的架构名称是**dbo**。 请注意，您必须具有指定架构名称所需的权限。 如果省略架构名称，将使用数据库用户的默认架构。  
  
```  
CREATE TABLE dbo.Points   
(ID int IDENTITY(1,1) PRIMARY KEY, PointValue Point)  
```  
  
## <a name="creating-indexes-on-udt-columns"></a>对 UDT 列创建索引  
 有两个用于为 UDT 列编制索引的选项：  
  
-   为整个值编制索引。 在此情况下，如果 UDT 是二进制排序的，则可以通过使用 CREATE INDEX [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句对整个 UDT 列创建索引。  
  
-   对 UDT 表达式编制索引。 您可以对 UDT 表达式在持久计算列上创建索引。 该 UDT 表达式可以是 UDT 的某一字段、方法或属性。 该表达式必须是确定性的并且不得执行数据访问。  
  
 有关详细信息，请参阅[clr 用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)并[CREATE INDEX &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)。  
  
## <a name="see-also"></a>请参阅  
 [使用 SQL Server 中的用户定义类型](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)  
  
  
