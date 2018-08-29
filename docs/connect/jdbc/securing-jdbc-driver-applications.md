---
title: 保护 JDBC 驱动程序应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 90724ec6-a9cb-43ef-903e-793f89410bc0
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 091c7a2e7df6a073f7404af9b512a9b6404e6324
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785733"
---
# <a name="securing-jdbc-driver-applications"></a>保护 JDBC Driver 应用程序

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

增强 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 应用程序的安全性并不仅仅是避免一般的代码缺陷这一个方面。 访问数据的应用程序具有许多潜在的故障点，攻击者可以利用它们检索、操纵或破坏敏感数据。 重要的是了解安全性的各个环节，包括从应用程序设计阶段的威胁建模到应用程序最终部署的整个过程，以及应用程序的长期持续维护工作。  
  
本部分的各个主题介绍一些常见的安全事项，包括连接字符串、验证用户输入以及一般的应用程序安全性。  
  
## <a name="in-this-section"></a>本节内容  
  
| 主题                                                                            | 描述                                                                                                                                                           |
| -------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [保护连接字符串](../../connect/jdbc/securing-connection-strings.md) | 描述有助于保护可用来连接到数据源的信息的各种技术。                                                                                    |
| [验证用户输入](../../connect/jdbc/validating-user-input.md)             | 描述验证用户输入的技术。                                                                                                                          |
| [应用程序安全性](../../connect/jdbc/application-security.md)               | 描述如何使用 Java 策略权限来帮助保护 JDBC Driver 应用程序。                                                                                |
| [使用 SSL 加密](../../connect/jdbc/using-ssl-encryption.md)               | 描述如何使用安全套接字层 (SSL) 与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库之间建立安全通信通道。 |
| [FIPS 模式](../../connect/jdbc/fips-mode.md)                                     | 介绍如何使用 JDBC 驱动程序以 FIPS 兼容模式。                                                                                                              |
  
## <a name="see-also"></a>另请参阅  

 [JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
