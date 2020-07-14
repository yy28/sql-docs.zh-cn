---
title: 创建本机编译的存储过程 | Microsoft Docs
description: 了解仅本机编译的存储过程支持的 Transact-SQL 功能。 了解如何在 SQL Server 中创建本机编译的存储过程。
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e6b34010-cf62-4f65-bbdf-117f291cde7b
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5ef2ee1bbc863de8f3be94733beac3f04fa90b3c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723289"
---
# <a name="creating-natively-compiled-stored-procedures"></a>创建本机编译的存储过程
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

本机编译的存储过程未实现完整 [!INCLUDE[tsql](../../includes/tsql-md.md)] 可编程性和查询外围应用。 某些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 构造不能在本机编译的存储过程内使用。 有关详细信息，请参阅 [本机编译的 T-SQL 模块支持的功能](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)。  
  
但是，有几个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能，仅本机编译的存储过程支持这些功能：  
  
-   原子块。 有关详细信息，请参阅 [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)。  
  
-   参数和变量的 NOT NULL 约束。 不能将 **NULL** 值分配给声明为 **NOT NULL**的参数或变量。 有关详细信息，请参阅 [DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)。  
  
    -   CREATE PROCEDURE dbo.myproc (@myVarchar  varchar(32)  **not null**) ...  
  
    -   DECLARE @myVarchar  varchar(32)  **not null = "Hello"** ; -- *（必须初始化为一个值。）*  
  
    -   SET @myVarchar **= null**; -- *（编译，但在运行时失败。）*  
  
-   本机编译存储过程的架构绑定。  
  
使用 [CREATE PROCEDURE (Transact-SQL)](../../t-sql/statements/create-procedure-transact-sql.md) 创建本机编译的存储过程。 下面的示例显示内存优化表以及用于将行插入表的本机编译存储过程。  
  
```sql  
CREATE TABLE [dbo].[T2] (  
  [c1] [int] NOT NULL, 
  [c2] [datetime] NOT NULL,
  [c3] nvarchar(5) NOT NULL, 
  CONSTRAINT [PK_T1] PRIMARY KEY NONCLUSTERED ([c1])  
  ) WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
CREATE PROCEDURE [dbo].[usp_2] (@c1 int, @c3 nvarchar(5)) 
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
)  
  DECLARE @c2 datetime = GETDATE();  
  INSERT INTO [dbo].[T2] (c1, c2, c3) values (@c1, @c2, @c3);  
END  
GO  
```  
 
在代码示例中， **NATIVE_COMPILATION** 指示此 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程是本机编译的存储过程。 以下选项是必需的：  
  
|选项|说明|  
|------------|-----------------|  
|**SCHEMABINDING**|本机编译的存储过程必须绑定到其引用的对象的架构。 这意味着不能删除该过程引用的表。 在该过程中引用的表必须包括其架构名称，并且在查询中不允许使用通配符 (\*)（意味着没有 `SELECT * from...`）。 此版本的**中的本机编译存储过程仅支持** SCHEMABINDING [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**BEGIN ATOMIC**|本机编译的存储过程正文必须由恰好一个原子块构成。 原子块确保存储过程的原子执行。 如果在活动事务的上下文外调用该过程，它将开始一个新事务，这个新事务在原子块的末尾提交。 本机编译存储过程中的原子块具有两个必需的选项：<br /><br /> **TRANSACTION ISOLATION LEVEL**。 有关支持的隔离级别的信息，请参阅 [内存优化表的事务隔离级别](https://msdn.microsoft.com/library/8a6a82bf-273c-40ab-a101-46bd3615db8a) 。<br /><br /> **LANGUAGE**。 存储过程的语言必须设置为可用语言或语言别名之一。|  
  
## <a name="see-also"></a>另请参阅  
 [本机编译的存储过程](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
