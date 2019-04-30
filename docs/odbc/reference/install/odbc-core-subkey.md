---
title: ODBC 核心子项 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 5c95c4e28a5f32131307daeaa61e214af887b577
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63069693"
---
# <a name="odbc-core-subkey"></a>ODBC 核心子项
在 ODBC 核心子项下的值提供的核心组件 （驱动程序管理器、 光标库、 安装程序 DLL，等） 的使用计数。 下表中显示此值的格式。  
  
|“属性”|数据类型|数据|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*计数*|  
  
 例如，假设三个不同的应用程序和两个不同的驱动程序的安装程序安装了 ODBC 核心组件。 在 ODBC 核心子项下的值将是：  
  
```  
UsageCount : REG_DWORD : 0x5  
```
