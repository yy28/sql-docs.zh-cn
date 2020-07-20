---
title: “允许 PolyBase 导出”配置选项 | Microsoft Docs
description: 在 SQL Server 设置中设置 `allow polybase export` 配置选项
ms.custom: ''
ms.date: 07/10/2020
ms.prod: sql
ms.prod_service: ''
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c25a7e42b55561ed6337281497e847999d722292
ms.sourcegitcommit: dacd9b6f90e6772a778a3235fb69412662572d02
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2020
ms.locfileid: "86279644"
---
# <a name="set-allow-polybase-export-configuration-option"></a>设置 `allow polybase export` 配置选项

[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

可使用 `allow polybase export` 服务器配置选项通过 `INSERT` 插入 Hadoop 外部表。 

此功能不支持插入到其他外部数据源。

 下表中列出了该选项的可能值： 

| 值 | 含义                                |
|-------|----------------------------------------|
| 0     | 已禁用。 这是默认设置。 |
| 1     | 已启用                                |


设置立即生效。

## <a name="example"></a>示例

以下示例将启用此设置。

```sql
sp_configure 'show advanced options', 1;
GO
RECONFIGURE;
GO
sp_configure 'allow polybase export', 0;
GO
RECONFIGURE;
GO
```

## <a name="next-steps"></a>后续步骤

 [导出数据](../../relational-databases/polybase/polybase-configure-hadoop.md#exporting-data)