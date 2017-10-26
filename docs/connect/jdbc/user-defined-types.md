---
title: "用户定义的类型 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 19a71b27-b788-43a3-a76d-fe3001a6f016
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ed2b0bb8227a1b430bcd30b1d41460862c8db325
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="user-defined-types"></a>用户定义的类型
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  中引入了用户定义类型 (Udt)[!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]使开发人员能够通过将存储在公共语言运行时 (CLR) 对象扩展服务器的标量类型系统[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。 Udt 可以包含多个元素，并且可以有与传统别名数据类型，组成的一个不同的行为，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]系统数据类型。 以前 UDT 的最大大小限制为 8 KB。 在[!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]，Udt 大于 64 千字节为单位的添加了支持。 从 3.0 版开始，JDBC 驱动程序还支持在指定 UserDefined 格式时大于 64 KB 的 UDT。  
  
 对于小于或等于 8,000 字节的 UDT 在行为上没有变化，但支持更大的 UDT 并且将其大小报告为“无限制”。  
  
## <a name="see-also"></a>另请参阅  
 [了解 JDBC 驱动程序数据类型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  

