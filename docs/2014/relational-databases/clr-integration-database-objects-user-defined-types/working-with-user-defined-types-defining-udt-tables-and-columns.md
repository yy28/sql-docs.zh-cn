---
title: 定义 UDT 表和列 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 1b87e497c6610a2d75daa9432246e4f4b4690bab
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62874449"
---
# <a name="defining-udt-tables-and-columns"></a>定义 UDT 表和列
  一旦包含用户定义类型（UDT）定义的程序集已在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库中注册，它就可以在列定义中使用。  
  
## <a name="creating-tables-with-udts"></a>使用 UDT 创建表  
 没有用于在表中创建 UDT 列的特殊语法。 您可以在某一列定义中使用 UDT 的名称，就像它是某一内部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型一样。 下面的 CREATE TABLE [!INCLUDE[tsql](../../includes/tsql-md.md)]语句将创建一个名为**Points**的表，其中包含一个名为 **"ID"** 的列，该列定义为`int`标识列和表的主键。 第二列的名称为**PointValue**，数据类型为**Point**。 本示例中使用的架构名称为**dbo**。 请注意，您必须具有指定架构名称所需的权限。 如果省略架构名称，将使用数据库用户的默认架构。  
  
```  
CREATE TABLE dbo.Points   
(ID int IDENTITY(1,1) PRIMARY KEY, PointValue Point)  
```  
  
## <a name="creating-indexes-on-udt-columns"></a>对 UDT 列创建索引  
 有两个用于为 UDT 列编制索引的选项：  
  
-   为整个值编制索引。 在此情况下，如果 UDT 是二进制排序的，则可以通过使用 CREATE INDEX [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句对整个 UDT 列创建索引。  
  
-   对 UDT 表达式编制索引。 您可以对 UDT 表达式在持久计算列上创建索引。 该 UDT 表达式可以是 UDT 的某一字段、方法或属性。 该表达式必须是确定性的并且不得执行数据访问。  
  
 有关详细信息，请参阅[CLR 用户定义类型](clr-user-defined-types.md)和[CREATE INDEX &#40;transact-sql&#41;](/sql/t-sql/statements/create-index-transact-sql)。  
  
## <a name="see-also"></a>另请参阅  
 [使用 SQL Server 中的用户定义类型](working-with-user-defined-types-in-sql-server.md)  
  
  
