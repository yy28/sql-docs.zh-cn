---
title: ODBC 核心子项 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 915c42e52c768a1b43a00b1a537a6885269f8a85
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="odbc-core-subkey"></a>ODBC 核心子项
ODBC 核心子项下的值提供的核心组件 （驱动程序管理器、 光标库，安装程序 DLL，等） 的使用计数。 下表中显示此值的格式。  
  
|名称|数据类型|Data|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*计数*|  
  
 例如，假设由三个不同的应用程序和两个不同的驱动程序的安装程序安装的 ODBC 核心组件。 将 ODBC 核心子项下的值：  
  
```  
UsageCount : REG_DWORD : 0x5  
```
