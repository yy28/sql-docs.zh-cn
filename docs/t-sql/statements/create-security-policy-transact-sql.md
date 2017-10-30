---
title: "创建安全策略 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SECURITY_POLICY_TSQL
- CREATE SECURITY
- SECURITY
- CREATE_SECURITY_POLICY_TSQL
- CREATE_SECURITY_TSQL
- SECURITY POLICY
- SECURITY_TSQL
- CREATE SECURITY POLICY
dev_langs:
- TSQL
helpviewer_keywords:
- RLS
- CREATE SECURITY POLICY statement
- Row-Level Security
ms.assetid: d6ab70ee-0fa2-469c-96f6-a3c16d673bc8
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 53292dc3f9f5cbd36913276496084d4648f13520
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-security-policy-transact-sql"></a>创建安全策略 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  创建行级别安全性的安全策略。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```     
CREATE SECURITY POLICY [schema_name. ] security_policy_name    
    { ADD [ FILTER | BLOCK ] } PREDICATE tvf_schema_name.security_predicate_function_name   
      ( { column_name | arguments } [ , …n] ) ON table_schema_name. table_name    
      [ <block_dml_operation> ] , [ , …n] 
    [ WITH ( STATE = { ON | OFF }  [,] [ SCHEMABINDING = { ON | OFF } ] ) ]  
    [ NOT FOR REPLICATION ] 
[;]  
  
<block_dml_operation>  
    [ { AFTER { INSERT | UPDATE } }   
    | { BEFORE { UPDATE | DELETE } } ]  
```  
  
## <a name="arguments"></a>参数  
 *security_policy_name*  
 安全策略的名称。 安全策略名称必须符合有关标识符的规则，并且在数据库中以及对其架构来说必须是唯一的。  
  
 *schema_name*  
 是安全策略所属架构的名称。 *schema_name*由于架构绑定，所以需。  
  
 [筛选器 |块]  
 安全谓词绑定到目标表的函数的类型。 筛选器谓词以静默方式筛选可用于读取操作的行。 块显式谓词违反该谓词函数的块写入操作。  
  
 *tvf_schema_name.security_predicate_function_name*  
 是将用作谓词的内联表值函数，并且将强制用于对目标表的查询。 最多能为针对特定表的特定 DML 操作定义一个安全谓词。 必须使用 SCHEMABINDING 选项创建内联表值函数。  
  
 { *column_name* | *参数*}  
 用作安全谓词函数的参数的列名和表达式。 目标表上的任意列都能用作谓词函数的参数。 可以使用包含文字、内置的表达式和使用算术运算符的表达式。  
  
 *table_schema_name.table_name*  
 是将要应用安全谓词的目标表。 多个已禁用的安全策略可以针对单个表为特定的 DML 操作，但只有一个可以在任何给定时间启用它。  
  
 *\<block_dml_operation >*将为其应用阻止谓词的特定 DML 操作。 后指定后 DML 操作被执行 （插入或更新），该谓词，计算上的行的值。 之前指定 DML 操作之前执行 （UPDATE 或 DELETE） 将上的行的值计算谓词。 如果不指定的任何操作，则谓词将应用于所有操作。  
  
 [状态 = {ON |**OFF** }]  
 使安全策略能够或禁止其对目标表强制执行其安全谓词。 如果未指定，则将启用正在创建的安全性策略。  
  
 [SCHEMABINDING = {ON |关闭}]  
 指示是否必须使用 SCHEMABINDING 选项创建的策略中的所有谓词函数。 默认情况下，必须使用 SCHEMABINDING 创建所有函数。  
  
 NOT FOR REPLICATION  
 指示当复制代理修改目标对象时不应执行安全策略。 有关详细信息，请参阅[控制同步期间触发器和约束的行为（复制 Transact-SQL 编程）](../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)。  
  
 [*table_schema_name*。]*table_name*  
 是将要应用安全谓词的目标表。 多个禁用的安全策略能以单个表为目标，但是在任何给定时间只能启用一个。  
  
## <a name="remarks"></a>注释  
 在使用内存优化表的谓词函数，你必须纳入**SCHEMABINDING**并用**WITH NATIVE_COMPILATION**编译提示。  
  
 在执行相应的 DML 操作后，将计算阻止谓词。 因此，READ UNCOMMITTED 查询可以看到将回滚的临时值。  
  
## <a name="permissions"></a>Permissions  
 要求对架构具有 ALTER ANY SECURITY POLICY 权限和 ALTER 权限。  
  
 另外，每个添加的谓词都需要以下权限：  
  
-   针对被用作谓词的函数的 SELECT 和 REFERENCES 权限。  
  
-   针对绑定到策略的目标表的 REFERENCES 权限。  
  
-   针对目标表上被用作参数的每一列的 REFERENCES 权限。  
  
## <a name="examples"></a>示例  
 以下示例展示了 **CREATE SECURITY POLICY** 语法的使用。 有关完整的安全策略方案的示例，请参阅[行级别安全性](../../relational-databases/security/row-level-security.md)。  
  
### <a name="a-creating-a-security-policy"></a>A. 创建安全策略  
 以下语法为 Customer 表创建了带有一个筛选器谓词的安全策略，并使安全策略处于禁用状态。  
  
```  
CREATE SECURITY POLICY [FederatedSecurityPolicy]   
ADD FILTER PREDICATE [rls].[fn_securitypredicate]([CustomerId])   
ON [dbo].[Customer];  
```  
  
### <a name="b-creating-a-policy-that-affects-multiple-tables"></a>B. 创建影响多个表的策略  
 以下语法对三个不同的表创建了带有三个筛选谓词的安全策略，并启用了该安全策略。  
  
```  
CREATE SECURITY POLICY [FederatedSecurityPolicy]   
ADD FILTER PREDICATE [rls].[fn_securitypredicate1]([CustomerId])   
    ON [dbo].[Customer],  
ADD FILTER PREDICATE [rls].[fn_securitypredicate1]([VendorId])   
    ON [dbo].[ Vendor],  
ADD FILTER PREDICATE [rls].[fn_securitypredicate2]([WingId])   
    ON [dbo].[Patient]  
WITH (STATE = ON);  
```  
  
### <a name="c-creating-a-policy-with-multiple-types-of-security-predicates"></a>C. 使用多个类型的安全谓词创建策略  
 将筛选器谓词和阻止谓词添加到 Sales 表中。  
  
```  
CREATE SECURITY POLICY rls.SecPol  
    ADD FILTER PREDICATE rls.tenantAccessPredicate(TenantId) ON dbo.Sales,  
    ADD BLOCK PREDICATE rls.tenantAccessPredicate(TenantId) ON dbo.Sales AFTER INSERT;  
```  
  
## <a name="see-also"></a>另请参阅  
 [行级安全性](../../relational-databases/security/row-level-security.md)   
 [ALTER SECURITY POLICY (Transact-SQL)](../../t-sql/statements/alter-security-policy-transact-sql.md)   
 [DROP SECURITY POLICY (Transact-SQL)](../../t-sql/statements/drop-security-policy-transact-sql.md)   
 [sys.security_policies (Transact-SQL)](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [sys.security_predicates &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)  
  
  


