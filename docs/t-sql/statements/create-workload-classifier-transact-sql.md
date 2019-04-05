---
title: CREATE WORKLOAD Classifier (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD CLASSIFIER
- WORKLOAD_CLASSIFIER_TSQL
- CREATE WORKLOAD CLASSIFIER
- CREATE_WORKLOAD_CLASSIFIER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE WORKLOAD CLASSIFIER statement
ms.assetid: ''
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: b925917c7d8ef55d687372e0854b136d365de0ac
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538209"
---
# <a name="create-workload-classifier-transact-sql-preview"></a>CREATE WORKLOAD CLASSIFIER (Transact-SQL)（预览）

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

创建工作负荷管理分类器。  分类器将传入请求分配给工作负荷组，并根据分类器语句定义中指定的参数分配重要性。  对提交的每个请求评估分类器。  如果请求与分类器不匹配，则将其分配给默认工作负荷组。  默认工作负载组是 smallrc 资源类。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>语法

```
CREATE WORKLOAD CLASSIFIER classifier_name  
WITH  
    ( WORKLOAD_GROUP = 'name'  
     ,MEMBERNAME = 'security_account'
 [ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL (default) | ABOVE_NORMAL | HIGH }])
[;]
```

## <a name="arguments"></a>参数

 classifier_name  
 指定用于标识工作负荷分类器的名称。  classifier_name 为 sysname。  最长可为 128 个字符，并且在实例中必须是唯一的。

WORKLOAD_GROUP = 'name' 当分类器规则满足条件时，名称将请求映射到工作负荷组。  名称为 sysname。  它最多可以包含 128 个字符，并且在创建分类器时必须是有效的工作负荷组名称。

WORKLOAD_GROUP 应映射到现有资源类：

|静态资源类|动态资源类|
|------------------------|-----------------------|
|staticrc10|smallrc|
|staticrc20|mediumrc|
|staticrc30|largerc|
|staticrc40|xlargerc|
|staticrc50||
|staticrc60||
|staticrc70||
|staticrc80||

MEMBERNAME = 'security_account' 这是添加到角色的安全帐户。  Security_account 为 sysname，没有默认值。 Security_account 可以是数据库用户、数据库角色、Azure Active Directory 登录名或 Azure Active Directory 组。

IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH } 指定请求的相对重要性。  重要性为以下值之一：

- LOW
- BELOW_NORMAL
- NORMAL（默认值）
- ABOVE_NORMAL
- HIGH  

重要性会影响请求的顺序，导致首先访问资源和锁定。

如果用户是具有在多个分类器中分配或匹配的不同资源类的多个角色的成员，则会授予此用户最高的资源类分配。 有关详细信息，请参阅[工作负荷分类](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification#classification-precedence)

## <a name="permissions"></a>权限

 需要 CONTROL DATABASE 权限。  
  
## <a name="examples"></a>示例

 下面的示例演示了如何创建名为 `wgcELTRole` 的工作负荷分类器。 它使用 staticrc20 工作负荷组和用户 `ELTRole`，并将重要性设置为 `above_normal`。

```sql
CREATE WORKLOAD CLASSIFIER wgcELTRole
  WITH (WORKLOAD_GROUP = 'staticrc20'
       ,MEMBERNAME = 'ELTRole'
      ,IMPORTANCE = above_normal);
```

## <a name="see-also"></a>另请参阅

[DROP WORKLOAD CLASSIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-classifier-transact-sql.md)</br>
目录视图 [sys.workload_management_workload_classifier_details](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifier-details-transact-sql.md)</br>
目录视图 [sys.workload_management_workload_classifiers](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifiers-transact-sql.md)
[SQL 数据仓库分类](/azure/sql-data-warehouse/classification)
