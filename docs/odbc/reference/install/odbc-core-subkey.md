---
title: "ODBC 核心子项 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ad7a45f0f3272e1e2d7ae799ab1ca86bfb90b9be
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-core-subkey"></a>ODBC 核心子项
ODBC 核心子项下的值提供的核心组件 （驱动程序管理器、 光标库，安装程序 DLL，等） 的使用计数。 下表中显示此值的格式。  
  
|Name|数据类型|data|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*计数*|  
  
 例如，假设由三个不同的应用程序和两个不同的驱动程序的安装程序安装的 ODBC 核心组件。 将 ODBC 核心子项下的值：  
  
```  
UsageCount : REG_DWORD : 0x5  
```

