---
title: "更改安全策略 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_SECURITY_POLICY_TSQL
- ALTER SECURITY POLICY
- ALTER_SECURITY_TSQL
- ALTER SECURITY
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER SECURITY POLICY statement
ms.assetid: a8efc37e-113d-489c-babc-b914fea2c316
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f5ce90660a43e5285735a74a01b560ec210ba3f0
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="alter-security-policy-transact-sql"></a>更改安全策略 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  更改安全策略。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
ALTER SECURITY POLICY schema_name.security_policy_name   
    (  
        { ADD { FILTER | BLOCK } PREDICATE tvf_schema_name.security_predicate_function_name   
           ( { column_name | arguments } [ , …n ] ) ON table_schema_name.table_name   
           [ <block_dml_operation> ]  }   
        | { ALTER { FILTER | BLOCK } PREDICATE tvf_schema_name.new_security_predicate_function_name   
             ( { column_name | arguments } [ , …n ] ) ON table_schema_name.table_name   
           [ <block_dml_operation> ] }  
        | { DROP { FILTER | BLOCK } PREDICATE ON table_schema_name.table_name }   
        | [ <additional_add_alter_drop_predicate_statements> [ , ...n ] ]  
    )    [ WITH ( STATE = { ON | OFF } ]  
    [ NOT FOR REPLICATION ]  
[;]  
  
<block_dml_operation>  
    [ { AFTER { INSERT | UPDATE } }   
    | { BEFORE { UPDATE | DELETE } } ]  
```  
  
## <a name="arguments"></a>参数  
 security_policy_name  
 安全策略的名称。 安全策略名称必须符合有关标识符的规则，并且在数据库中以及对其架构来说必须是唯一的。  
  
 schema_name  
 是安全策略所属架构的名称。 *schema_name*由于架构绑定，所以需。  
  
 [筛选器 |块]  
 安全谓词绑定到目标表的函数的类型。 筛选器谓词以静默方式筛选可用于读取操作的行。 块显式谓词违反该谓词函数的块写入操作。  
  
 tvf_schema_name.security_predicate_function_name  
 是将用作谓词的内联表值函数，并且将强制用于对目标表的查询。 最多能为针对特定表的特定 DML 操作定义一个安全谓词。 必须使用 SCHEMABINDING 选项创建内联表值函数。  
  
 { column_name | arguments }  
 用作安全谓词函数的参数的列名和表达式。 目标表上的任意列都能用作谓词函数的参数。 可以使用包含文字、内置的表达式和使用算术运算符的表达式。  
  
 *table_schema_name.table_name*  
 是将要应用安全谓词的目标表。 多个已禁用的安全策略可以针对单个表为特定的 DML 操作，但只有一个可以在任何给定时间启用它。  
  
 *\<block_dml_operation >*  
 将为其应用阻止谓词的特定 DML 操作。 后指定后 DML 操作被执行 （插入或更新），该谓词，计算上的行的值。 之前指定 DML 操作之前执行 （UPDATE 或 DELETE） 将上的行的值计算谓词。 如果不指定的任何操作，则谓词将应用于所有操作。  
  
 无法更改为其将应用阻止谓词，该操作，因为该操作用于唯一标识该谓词。 相反，您必须删除该谓词，并添加一个新的新操作。  
  
 WITH ( STATE = { ON | OFF } )  
 使安全策略能够或禁止其对目标表强制执行其安全谓词。 如果不指定，则正在创建的安全性策略会被禁用。  
  
 NOT FOR REPLICATION  
 指示当复制代理修改目标对象时不应执行安全策略。 有关详细信息，请参阅[控制同步期间触发器和约束的行为（复制 Transact-SQL 编程）](../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md)。  
  
 table_schema_name.table_name  
 是将要应用安全谓词的目标表。 多个禁用的安全策略能以单个表为目标，但是在任何给定时间只能启用一个。  
  
## <a name="remarks"></a>Remarks  
 ALTER SECURITY POLICY 语句位于事务范围内。 如果对事务进行回滚，也将对该语句进行回滚。  
  
 安全策略时使用内存优化表的谓词函数，必须包括**SCHEMABINDING**并用**WITH NATIVE_COMPILATION**编译提示。 无法使用 ALTER 语句更改 SCHEMABINDING 参数，因为它将应用于的所有谓词。 若要更改架构绑定必须删除并重新创建安全策略。  
  
 在执行相应的 DML 操作后，将计算阻止谓词。 因此，READ UNCOMMITTED 查询可以看到将回滚的临时值。  
  
## <a name="permissions"></a>权限  
 需要 ALTER ANY SECURITY POLICY 权限。  
  
 另外，每个添加的谓词都需要以下权限：  
  
-   针对被用作谓词的函数的 SELECT 和 REFERENCES 权限。  
-   针对绑定到策略的目标表的 REFERENCES 权限。  
-   针对目标表上被用作参数的每一列的 REFERENCES 权限。  
  
## <a name="examples"></a>示例  
 下面的示例演示了利用**ALTER SECURITY POLICY**语法。 有关完整的安全策略方案的示例，请参阅[行级别安全性](../../relational-databases/security/row-level-security.md)。  
  
### <a name="a-adding-an-additional-predicate-to-a-policy"></a>A. 向策略添加其他谓词  
 以下语法更改安全策略，同时添加一个筛选器谓词到 `mytable` 表。  
  
```  
ALTER SECURITY POLICY pol1   
    ADD FILTER PREDICATE schema_preds.SecPredicate(column1)   
    ON myschema.mytable;  
```  
  
### <a name="b-enabling-an-existing-policy"></a>B. 启用一个现有策略  
 以下示例使用了 ALTER 语法来启用安全策略。  
  
```  
ALTER SECURITY POLICY pol1 WITH ( STATE = ON );  
```  
  
### <a name="c-adding-and-dropping-multiple-predicates"></a>C. 添加和删除多个谓词  
 以下语法更改安全策略，同时添加筛选器谓词到 `mytable1` 和 `mytable3` 表，并删除 `mytable2` 表上的筛选器谓词。  
  
```  
ALTER SECURITY POLICY pol1  
ADD FILTER PREDICATE schema_preds.SecPredicate1(column1)   
    ON myschema.mytable1,  
DROP FILTER PREDICATE   
    ON myschema.mytable2,  
ADD FILTER PREDICATE schema_preds.SecPredicate2(column2, 1)   
    ON myschema.mytable3;  
```  
  
### <a name="d-changing-the-predicate-on-a-table"></a>D. 更改表中谓词  
 下面的语法可将 mytable 表中的现有筛选器谓词更改为 SecPredicate2 函数。  
  
```  
ALTER SECURITY POLICY pol1  
    ALTER FILTER PREDICATE schema_preds.SecPredicate2(column1)  
        ON myschema.mytable;  
```  
  
### <a name="e-changing-a-block-predicate"></a>E. 更改的 block 谓词  
 更改表上的操作的块将在谓词函数。  
  
```  
ALTER SECURITY POLICY rls.SecPol  
    ALTER BLOCK PREDICATE rls.tenantAccessPredicate_v2(TenantId) 
    ON dbo.Sales AFTER INSERT;  
```  
  
## <a name="see-also"></a>另请参阅  
 [行级安全性](../../relational-databases/security/row-level-security.md)   
 [CREATE SECURITY POLICY (Transact-SQL)](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [DROP SECURITY POLICY (Transact-SQL)](../../t-sql/statements/drop-security-policy-transact-sql.md)   
 [sys.security_policies (Transact-SQL)](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [sys.security_predicates &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)  
  
  
