---
description: ODBC 核心子项
title: ODBC Core 子项 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37948c46d6a717975902bc2109ece2aea02b0129
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499732"
---
# <a name="odbc-core-subkey"></a>ODBC 核心子项
ODBC Core 子项下的值提供了 (驱动程序管理器、游标库、安装程序 DLL) 的核心组件的使用计数。 下表显示了此值的格式。  
  
|名称|数据类型|数据|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*计数*|  
  
 例如，假设已由安装程序为三个不同的应用程序和两个不同的驱动程序安装了 ODBC 核心组件。 ODBC Core 子项下的值将为：  
  
```  
UsageCount : REG_DWORD : 0x5  
```
