---
description: 取消显示恢复模式错误 - 服务器配置选项
title: 取消显示恢复模式错误 - 服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 07/20/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 942dfc62bd55d1843babb78d89b95ad602f3d938
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670740"
---
# <a name="suppress-recovery-model-errors-server-configuration-option"></a>取消显示恢复模式错误服务器配置选项

[!INCLUDE[tsql-appliesto-xxxxxx-asdbmi-xxxx-xxx-md.md](../../includes/tsql-appliesto-xxxxxx-asdbmi-xxxx-xxx-md.md)]

SQL Server [恢复模型](../../relational-databases/backup-restore/recovery-models-sql-server.md)控制事务日志维护。 完整恢复模式可确保不会因数据文件丢失或损坏而丢失任何工作，并且支持恢复到备份保留策略内的任意时间点。 完整恢复模式是默认的，并且 SQL 托管实例仅支持恢复模式。 尝试在 SQL 托管实例中更改恢复模式将返回错误消息。

使用“取消显示恢复模式错误”高级配置选项即可指定 SQL 托管实例上执行的用于更改数据库恢复模式的命令仅返回错误还是仅返回警告。 在 SQL 托管实例上将此选项设置为 1 (ON) 时，执行命令 ALTER DATABASE SET RECOVERY 将不会更改数据库的恢复模式，尽管如此，该命令不会返回错误，而是返回警告消息。 在 SQL 托管实例上将此选项设置为 0 (OFF) 时，执行命令 ALTER DATABASE SET RECOVERY 将返回错误消息。

虽然“取消显示恢复模式错误”选项不是关键或强制性需求，但它在旧版或第三方应用程序试图将恢复模式更改为“简单”或“批量记录”的情况下很有用。 恢复模式的更改是使用 SQL 托管实例的唯一阻碍时，启用“取消显示恢复模式错误”配置选项即可消除该阻碍。 如果更改应用程序代码的替代解决方案不可行或成本高昂，则此选项会特别有用。

## <a name="examples"></a>示例

以下示例取消显示与数据库恢复模式更改有关的错误消息，然后执行用于更改数据库恢复模式的命令，从而仅返回警告。 恢复模式实际上并未更改。 确保将 my_database 替换为实际的数据库名称。

```sql
-- Turn advanced configuration options on:
sp_configure 'show advanced options', 1 ;  
GO
RECONFIGURE ;  
GO

-- Enable suppression of error messages for recovery model change:
sp_configure 'suppress recovery model errors', 1 ;  
GO
RECONFIGURE ;  
GO

-- Execute command for changing recovery model to Simple:
ALTER DATABASE my_database SET RECOVERY SIMPLE;
GO
```

## <a name="see-also"></a>另请参阅

[服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)

[sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)

[RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)