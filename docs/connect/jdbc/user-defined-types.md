---
title: 用户定义的类型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 19a71b27-b788-43a3-a76d-fe3001a6f016
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 72dca79e295f54d4c01421ef79408008bd559210
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38039136"
---
# <a name="user-defined-types"></a>用户定义的类型
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  用户定义类型 (UDT) 是在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] 中引入的，以允许开发人员通过在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 数据库中存储公共语言运行时 (CLR) 对象来扩展服务器的标量类型系统。 UDT 可以包含多个元素，也可以具有多种行为，不同于传统的由单个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 系统数据类型组成的别名数据类型。 以前 UDT 的最大大小限制为 8 KB。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] 中，已经新增了对大于 64 KB 的 UDT 的支持。 从 3.0 版开始，JDBC 驱动程序还支持在指定 UserDefined 格式时大于 64 KB 的 UDT。  
  
 对于小于或等于 8,000 字节的 UDT 在行为上没有变化，但支持更大的 UDT 并且将其大小报告为“无限制”。  
  
## <a name="see-also"></a>另请参阅  
 [了解 JDBC 驱动程序数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
