---
title: ODBC 驱动程序子项 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], drivers subkey
- registry entries for components [ODBC], drivers subkey
- drivers subkey [ODBC]
ms.assetid: 8edbf68f-d05d-4d77-92f6-e9500008f520
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 43be1c5e75998903ff4e64fc5f4230818a873ffc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63281125"
---
# <a name="odbc-drivers-subkey"></a>ODBC 驱动程序子项
ODBC 驱动程序子项下的值列出已安装的驱动程序。 下表中显示这些值的格式。  
  
|“属性”|数据类型|数据|  
|----------|---------------|----------|  
|*driver-description*|REG_SZ|**安装**|  
  
 *驱动程序说明*由驱动程序开发人员定义名称。 它通常是与该驱动程序相关联的 DBMS 的名称。  
  
 例如，假设用于格式化的文本的文件和 SQL Server 安装了驱动程序。 ODBC 驱动程序子项下的值可能是：  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
