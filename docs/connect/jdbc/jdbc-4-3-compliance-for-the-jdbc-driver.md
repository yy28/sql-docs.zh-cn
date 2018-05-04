---
title: JDBC 4.3 JDBC 驱动程序的符合性 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33b218598871e570fa99d212d565c834718de1d9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC 4.3 JDBC 驱动程序的符合性
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

    
> [!NOTE]  
>  SQL server 的 Microsoft JDBC 驱动程序 6.4 之前的版本是符合的 Java 数据库连接 API 4.2 规范。 本节不适用于在 6.4 版本之前的版本。  
  
 目前，SQL server 的 Microsoft JDBC 驱动程序 6.4 是 Java 9 兼容，但不完全兼容的 Java 数据库连接 API 4.3 规范。 为新引入 Api 以 JDBC 4.3，如果不是所支持的驱动程序，该驱动程序将引发 SQLFeatureNotSupportedException。