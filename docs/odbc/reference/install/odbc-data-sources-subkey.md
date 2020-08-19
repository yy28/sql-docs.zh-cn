---
description: ODBC 数据源子项
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
ms.openlocfilehash: 9897c68d110f59d03ac8e1b3e403ed21844082fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448929"
---
# <a name="odbc-data-sources-subkey"></a>ODBC 数据源子项

子项下的值 `ODBC Data Sources` 列出数据源。 下表显示了这些值的格式。

| 名称 | 数据类型 | 数据 |
| :--- | :-------- | :--- |
| *数据源-名称* | REG_SZ | *驱动程序-说明* |
| &nbsp; | &nbsp; | &nbsp; |

*数据源名称*值由管理程序定义 (通常会提示用户) ，*驱动程序说明*由驱动程序开发人员定义 (它通常是与驱动程序) 关联的 DBMS 的名称。

例如，假设定义了三个数据源：清点，使用 SQL Server;使用 dBASE 的工资单;和使用带格式文本文件的人员。 子项下的值 `ODBC Data Sources` 可能如下所示：

```console
Inventory : REG_SZ : SQL Server
Payroll : REG_SZ : dBASE
Personnel : REG_SZ : Text
```
