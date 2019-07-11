---
title: sp_execute_remote （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sp_execute_remote
- sp_execute_remote_TSQL
helpviewer_keywords:
- remote execution
- queries, remote execution
ms.assetid: ca89aa4c-c4c1-4c46-8515-a6754667b3e5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 100da3bfaeee1c4b1e4dae00c96bcc08a763f3b3
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716608"
---
# <a name="spexecuteremote-azure-sql-database"></a>sp_execute_remote（Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  执行[!INCLUDE[tsql](../../includes/tsql-md.md)]上的单个远程 Azure SQL 数据库或数据库用作在水平分区方案中的分片集的语句。  
  
 存储的过程是弹性查询功能的一部分。  请参阅[Azure SQL 数据库弹性数据库查询概述](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)并[（横向分区） 的分片的弹性数据库查询](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-horizontal-partitioning/)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
sp_execute_remote [ @data_source_name = ] datasourcename  
[ , @stmt = ] statement  
[   
  { , [ @params = ] N'@parameter_name data_type [,...n ]' }   
     { , [ @param1 = ] 'value1' [ ,...n ] }  
]  
```  
  
## <a name="arguments"></a>参数  
 [ \@data_source_name = ] *datasourcename*  
 标识外部数据源执行该语句。 请参阅[创建外部数据源&#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)。 外部数据源可以是类型的"RDBMS"或"SHARD_MAP_MANAGER"。  
  
 [ \@stmt= ] *statement*  
 是一个 Unicode 字符串，包含[!INCLUDE[tsql](../../includes/tsql-md.md)]语句或批处理。 \@语句必须是 Unicode 常量或 Unicode 变量。 不允许使用更复杂的 Unicode 表达式（例如使用 + 运算符连接两个字符串）。 不允许使用字符常量。 如果指定 Unicode 常量，则它必须带有前缀**N**。例如，Unicode 常量**N 'sp_who'** 有效，但是字符常量 **'sp_who'** 不是。 字符串的大小仅受可用数据库服务器内存限制。 在 64 位服务器上的字符串的大小被限制为 2 GB 的最大大小**nvarchar （max)** 。  
  
> [!NOTE]  
>  \@语句可以包含的参数将同一个窗体作为变量名称，例如： `N'SELECT * FROM HumanResources.Employee WHERE EmployeeID = @IDParameter'`  
  
 包含在每个参数\@stmt 必须具有一个对应的条目，在这种\@params 参数定义列表和参数值列表。  
  
 [ \@params= ] N'\@*parameter_name**data_type* [ ,... *n* ] '  
 是一个字符串，它包含的定义中嵌入的所有参数\@stmt。字符串必须是 Unicode 常量或 Unicode 变量。 每个参数定义由参数名称和数据类型组成。 *n*是表示附加参数定义的占位符。 每个参数中指定\@中定义 stmtmust \@params。 如果[!INCLUDE[tsql](../../includes/tsql-md.md)]语句或批处理在\@stmt 不包含参数，\@参数不是必需的。 该参数的默认值为 NULL。  
  
 [ \@param1= ] '*value1*'  
 参数字符串中定义的第一个参数的值。 该值可以是 Unicode 常量，也可以是 Unicode 变量。 必须为包含在每个参数提供参数值\@stmt。值不需要[!INCLUDE[tsql](../../includes/tsql-md.md)]语句或批处理在\@stmt 不具有任何参数。  
  
 *n*  
 附加参数值的占位符。 这些值只能为常量或变量， 不能是很复杂的表达式（例如函数）或使用运算符生成的表达式。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或非零（失败）  
  
## <a name="result-sets"></a>结果集  
 返回的结果集的第一个 SQL 语句。  
  
## <a name="permissions"></a>权限  
 需要 `ALTER ANY EXTERNAL DATA SOURCE` 权限。  
  
## <a name="remarks"></a>备注  
 `sp_execute_remote` 必须按特定顺序输入参数，如上面的语法部分中所述。 如果这些参数的输入顺序不正确，则会显示一条错误消息。  
  
 `sp_execute_remote` 具有相同的行为[EXECUTE &#40;TRANSACT-SQL&#41; ](../../t-sql/language-elements/execute-transact-sql.md)对于批处理和名称的作用域。 TRANSACT-SQL 语句或批处理在 sp_execute_remote  *\@stmt*直到执行 sp_execute_remote 语句参数时才编译。  
  
 `sp_execute_remote` 将一个额外的列添加到名为 $ShardName，其中包含生成一行的远程数据库名称的结果集。  
  
 `sp_execute_remote` 可以使用类似于[sp_executesql &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md)。  
  
## <a name="examples"></a>示例  
### <a name="simple-example"></a>简单示例  
 下面的示例创建并远程数据库上执行简单的 SELECT 语句。  
  
```sql  
EXEC sp_execute_remote  
    N'MyExtSrc',  
    N'SELECT COUNT(w_id) AS Count_id FROM warehouse'   
```  
  
### <a name="example-with-multiple-parameters"></a>具有多个参数的示例  
在用户数据库中，指定管理员凭据，以便在 master 数据库中创建的数据库范围凭据。 创建外部数据源指向 master 数据库和指定的数据库范围凭据。 然后执行以下操作，在用户数据库中，示例`sp_set_firewall_rule`master 数据库中的过程。 `sp_set_firewall_rule`过程需要 3 个参数，并且需要`@name`参数为 Unicode。

```
EXEC sp_execute_remote @data_source_name  = N'PointToMaster', 
@stmt = N'sp_set_firewall_rule @name, @start_ip_address, @end_ip_address', 
@params = N'@name nvarchar(128), @start_ip_address varchar(50), @end_ip_address varchar(50)',
@name = N'TempFWRule', @start_ip_address = '0.0.0.2', @end_ip_address = '0.0.0.2';
```

## <a name="see-also"></a>另请参阅：

[CREATE DATABASE SCOPED CREDENTIAL](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
[CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)  
    
