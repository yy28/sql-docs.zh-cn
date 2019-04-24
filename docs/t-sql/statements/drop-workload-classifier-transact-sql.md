---
title: DROP WORKLOAD Classifier (Transact-SQL) | Microsoft Docs
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
- DROP_WORKLOAD_CLASSIFIER_TSQL
- DROP WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DROP WORKLOAD CLASSIFIER statement
ms.assetid: ''
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: a9ef53323d77f1439df5daf0fedc669fe380cb3f
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2019
ms.locfileid: "59581511"
---
# <a name="drop-workload-classifier-transact-sql-preview"></a>DROP WORKLOAD CLASSIFIER (Transact-SQL)（预览）

> [!Note]
> 可以在 SQL 数据仓库 Gen2 上预览工作负荷分类。 工作负荷管理分类和重要性预览适用于发布日期为 2019 年 4 月 9 日或更晚的内部版本。  用户应避免使用早于此日期的内部版本进行工作负荷管理测试。  若要确定内部版本是否支持工作负荷管理，请在连接到 SQL 数据仓库实例时运行 select @@version。

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

删除现有的用户定义的工作负荷管理分类器。  
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>语法  

```
DROP WORKLOAD CLASSIFIER classifier_name;
```

## <a name="arguments"></a>参数

classifier_name  
指定用于标识工作负荷分类器的名称。  classifier_name 为 sysname。  最长可为 128 个字符，并且在实例中必须是唯一的。
  
## <a name="remarks"></a>Remarks

系统工作负荷分类器上不允许使用 DROP WORKLOAD CLASSIFIER 语句。

如果请求正在运行或位于处于挂起状态的请求队列中，它们的分类保持不变，并且我们可以立即删除分类器。  删除和重新创建具有不同重要性的分类器不会影响已分类的请求。

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
