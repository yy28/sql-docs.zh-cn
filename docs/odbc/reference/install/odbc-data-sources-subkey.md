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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c5e97e643a78187b15e91833c832cd16ca435c7f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304050"
---
# <a name="odbc-data-sources-subkey"></a>ODBC 数据源子项

`ODBC Data Sources`子项下的值列出数据源。 下表显示了这些值的格式。

| 名称 | 数据类型 | 数据 |
| :--- | :-------- | :--- |
| *数据源-名称* | REG_SZ | *驱动程序-说明* |
| &nbsp; | &nbsp; | &nbsp; |

*数据源名称*值由管理程序（通常提示用户）定义，*驱动程序描述*由驱动程序开发人员定义（通常是与驱动程序相关联的 DBMS 的名称）。

例如，假设定义了三个数据源：清点，使用 SQL Server;使用 dBASE 的工资单;和使用带格式文本文件的人员。 `ODBC Data Sources`子项下的值可能如下所示：

```console
Inventory : REG_SZ : SQL Server
Payroll : REG_SZ : dBASE
Personnel : REG_SZ : Text
```
