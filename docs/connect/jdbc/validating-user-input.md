---
title: 验证用户输入 |Microsoft 文档
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
ms.topic: article
ms.assetid: 8aa867b0-e6f0-49eb-93d3-817ae2ed8f77
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e531c972fdcbec03a4b9195f35af1f8f651cd206
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MTE
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="validating-user-input"></a>验证用户输入
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  当您构造访问数据的应用程序时，应假定所有用户输入在获得验证之前都是恶意的。 未做到这一点可能导致应用程序易受攻击。 可能发生的一种类型的攻击称作 SQL 注入，其中恶意代码被添加到字符串中，然后这些字符串被传递到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 的实例中以进行分析和执行。 为了避免这种类型的攻击，应尽可能使用带参数的存储过程，并始终验证用户输入。  
  
 在客户端代码中验证用户输入是非常重要的，这样，您就无需浪费时间往返服务器。 在服务器上验证存储过程的参数以捕获无效的和跳过客户端验证的输入，这同样非常重要。  
  
 有关 SQL 注入和如何避免此攻击的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 联机丛书中的“SQL 注入”。 有关验证存储过程参数的详细信息，请参阅 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 联机丛书中的“存储过程 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)])”和从属主题。  
  
## <a name="see-also"></a>另请参阅  
 [保护 JDBC 驱动程序应用程序](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
