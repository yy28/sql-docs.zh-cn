---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98c9380083eb5a0ad796f436af271564676b757d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094010"
---
# <a name="odbc-core-subkey"></a>ODBC 核心子项
ODBC Core 子项下的值提供核心组件的使用计数（驱动程序管理器、游标库、安装程序 DLL 等）。 下表显示了此值的格式。  
  
|名称|数据类型|data|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*计数*|  
  
 例如，假设已由安装程序为三个不同的应用程序和两个不同的驱动程序安装了 ODBC 核心组件。 ODBC Core 子项下的值将为：  
  
```  
UsageCount : REG_DWORD : 0x5  
```
