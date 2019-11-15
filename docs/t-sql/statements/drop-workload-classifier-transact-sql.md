---
title: DROP WORKLOAD Classifier (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD CLASSIFIER
- WORKLOAD_CLASSIFIER_TSQL
- DROP_WORKLOAD_CLASSIFIER_TSQL
- DROP WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DROP WORKLOAD CLASSIFIER statement
author: ronortloff
ms.author: rortloff
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 5db3c50e4b0a21e2e1acf9512995870b62375dd8
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632835"
---
# <a name="drop-workload-classifier-transact-sql"></a>DROP WORKLOAD CLASSIFIER (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

删除现有的用户定义的工作负载管理分类器。  如果请求正在运行或位于处于挂起状态的请求队列中，它们的分类保持不变，并且我们可以立即删除分类器。 删除和重新创建具有不同重要性的分类器不会影响已分类的请求。
  
![“主题链接”图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>语法  

```
DROP WORKLOAD CLASSIFIER classifier_name;
```

## <a name="arguments"></a>参数

classifier_name   
指定用于标识工作负荷分类器的名称。
  
## <a name="permissions"></a>权限

需要 CONTROL DATABASE 权限。  
  
## <a name="examples"></a>示例

以下示例删除名为 `wgcELTROLE` 的工作负荷分类器。  

```sql
DROP WORKLOAD CLASSIFIER wgcELTRole;
```

> [!NOTE]
> 在没有匹配分类器的情况下提交的请求将被分类到默认工作负荷组。  默认工作负荷组是 smallrc 资源类。
  
## <a name="see-also"></a>另请参阅

[CREATE WORKLOAD CLASSIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-classifier-transact-sql.md)</br>
[SQL 数据仓库工作负荷分类](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
