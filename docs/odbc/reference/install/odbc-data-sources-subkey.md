---
title: ODBC 数据源子键 |微软文档
ms.custom: ''
ms.date: 09/23/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], for data sources
- data sources [ODBC], subkeys
- registry entries for data sources [ODBC], subkeys
ms.assetid: 0a8ccb80-c573-4418-84e5-f04a2b0e2ac1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c5e97e643a78187b15e91833c832cd16ca435c7f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304050"
---
# <a name="odbc-data-sources-subkey"></a>ODBC 数据源子键

`ODBC Data Sources`子键下的值列出数据源。 这些值的格式显示在下表中。

| 名称 | 数据类型 | 数据 |
| :--- | :-------- | :--- |
| *数据源名称* | REG_SZ | *驱动程序描述* |
| &nbsp; | &nbsp; | &nbsp; |

*数据源名称*值由管理程序定义（通常提示用户进行它），*驱动程序描述*由驱动程序开发人员定义（它通常是与驱动程序关联的 DBMS 的名称）。

例如，假设定义了三个数据源：使用 SQL Server 的清单;使用 dBASE 的薪资;和人员，它使用格式化的文本文件。 子键下`ODBC Data Sources`的值可能如下所示：

```console
Inventory : REG_SZ : SQL Server
Payroll : REG_SZ : dBASE
Personnel : REG_SZ : Text
```
