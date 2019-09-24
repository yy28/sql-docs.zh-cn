---
title: ODBC 数据源子项 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4d6d54d1fc7c7742bf94e91d7370f356e28b5624
ms.sourcegitcommit: 816ff47eeab157c66e0f75f18897a63dc8033502
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71207685"
---
# <a name="odbc-data-sources-subkey"></a>ODBC 数据源子项

`ODBC Data Sources`子项下的值列出数据源。 下表显示了这些值的格式。

| “属性” | 数据类型 | Data |
| :--- | :-------- | :--- |
| *data-source-name* | REG_SZ | *driver-description* |
| &nbsp; | &nbsp; | &nbsp; |

*数据源名称*值由管理程序（通常提示用户）定义，*驱动程序描述*由驱动程序开发人员定义（通常是与驱动程序相关联的 DBMS 的名称）。

例如，假设已经定义了三个数据源：清单，使用 SQL Server;使用 dBASE 的工资单;和使用带格式文本文件的人员。 `ODBC Data Sources`子项下的值可能如下所示：

```console
Inventory : REG_SZ : SQL Server
Payroll : REG_SZ : dBASE
Personnel : REG_SZ : Text
```
