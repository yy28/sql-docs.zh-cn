---
title: "JDBC 4.3 JDBC 驱动程序的符合性 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b3f678f33ec8f2c844bce14daa150f6c135744ff
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2018
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC 4.3 JDBC 驱动程序的符合性
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

    
> [!NOTE]  
>  SQL server 的 Microsoft JDBC 驱动程序 6.4 之前的版本是符合的 Java 数据库连接 API 4.2 规范。 本节不适用于在 6.4 版本之前的版本。  
  
 目前，SQL server 的 Microsoft JDBC 驱动程序 6.4 是 Java 9 兼容，但不完全兼容的 Java 数据库连接 API 4.3 规范。 为新引入 Api 以 JDBC 4.3，如果不是所支持的驱动程序，该驱动程序将引发 SQLFeatureNotSupportedException。