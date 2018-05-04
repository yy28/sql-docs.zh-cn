---
title: 保护 JDBC 驱动程序应用程序 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
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
ms.assetid: 90724ec6-a9cb-43ef-903e-793f89410bc0
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d777abfd88a6218e96ab1054d175f4e24e3b59d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="securing-jdbc-driver-applications"></a>保护 JDBC Driver 应用程序
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  增强的安全性[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]应用程序涉及多个避免常见的编码缺陷。 访问数据的应用程序具有许多潜在的故障点，攻击者可以利用它们检索、操纵或破坏敏感数据。 重要的是了解安全性的各个环节，包括从应用程序设计阶段的威胁建模到应用程序最终部署的整个过程，以及应用程序的长期持续维护工作。  
  
 本部分的各个主题介绍一些常见的安全事项，包括连接字符串、验证用户输入以及一般的应用程序安全性。  
  
## <a name="in-this-section"></a>本節內容  
  
|主题|Description|  
|-----------|-----------------|  
|[保护连接字符串](../../connect/jdbc/securing-connection-strings.md)|描述有助于保护可用来连接到数据源的信息的各种技术。|  
|[验证用户输入](../../connect/jdbc/validating-user-input.md)|描述验证用户输入的技术。|  
|[应用程序安全性](../../connect/jdbc/application-security.md)|描述如何使用 Java 策略权限来帮助保护 JDBC Driver 应用程序。|  
|[使用 SSL 加密](../../connect/jdbc/using-ssl-encryption.md)|描述如何建立具有的安全通信通道[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库使用安全套接字层 (SSL)。|  
|[FIPS 模式](../../connect/jdbc/fips-mode.md)|描述如何在与 FIPS 兼容模式下使用 JDBC 驱动程序。| 
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
