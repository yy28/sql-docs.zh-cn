---
title: ODBC 核心子键 |微软文档
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
ms.openlocfilehash: 9e6bfcf3c1efa87076e6d3e27a438cde6f794157
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304049"
---
# <a name="odbc-core-subkey"></a>ODBC 核心子项
ODBC Core 子键下的值提供核心组件（驱动程序管理器、游标库、安装程序 DLL 等）的使用计数。 此值的格式显示在下表中。  
  
|名称|数据类型|数据|  
|----------|---------------|----------|  
|使用情况计数|REG_DWORD|*count*|  
  
 例如，假设 ODBC Core 组件已由针对三个不同的应用程序和两个不同的驱动程序的安装程序安装。 ODBC 核心子键下的值是：  
  
```  
UsageCount : REG_DWORD : 0x5  
```
