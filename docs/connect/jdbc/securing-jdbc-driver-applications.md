---
title: 保护 JDBC 驱动程序应用程序 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 90724ec6-a9cb-43ef-903e-793f89410bc0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 61a17b302499f87d552ec61c90208effc688e164
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027747"
---
# <a name="securing-jdbc-driver-applications"></a>保护 JDBC 驱动程序应用程序

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

增强 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 应用程序的安全性并不仅仅是避免一般的代码缺陷这一个方面。 访问数据的应用程序具有许多潜在的故障点，攻击者可以利用它们检索、操纵或破坏敏感数据。 重要的是了解安全性的各个环节，包括从应用程序设计阶段的威胁建模到应用程序最终部署的整个过程，以及应用程序的长期持续维护工作。  
  
本部分的各个主题介绍一些常见的安全事项，包括连接字符串、验证用户输入以及一般的应用程序安全性。  
  
## <a name="in-this-section"></a>在本节中  
  
| 主题                                                                            | 说明                                                                                                                                                           |
| -------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [保护连接字符串](../../connect/jdbc/securing-connection-strings.md) | 描述有助于保护可用来连接到数据源的信息的各种技术。                                                                                    |
| [验证用户输入](../../connect/jdbc/validating-user-input.md)             | 描述验证用户输入的技术。                                                                                                                          |
| [应用程序安全性](../../connect/jdbc/application-security.md)               | 描述如何使用 Java 策略权限来帮助保护 JDBC Driver 应用程序。                                                                                |
| [使用 SSL 加密](../../connect/jdbc/using-ssl-encryption.md)               | 描述如何使用安全套接字层 (SSL) 与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库之间建立安全通信通道。 |
| [FIPS 模式](../../connect/jdbc/fips-mode.md)                                     | 介绍了如何在符合 FIPS 规定的模式下使用 JDBC 驱动程序。                                                                                                              |
  
## <a name="see-also"></a>另请参阅  

 [JDBC 驱动程序概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
