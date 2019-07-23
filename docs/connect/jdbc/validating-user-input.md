---
title: 正在验证用户输入 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8aa867b0-e6f0-49eb-93d3-817ae2ed8f77
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c2d890c4471dfeb85c1dd4f8f6f614a3b28cff90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003895"
---
# <a name="validating-user-input"></a>验证用户输入

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

当您构造访问数据的应用程序时，应假定所有用户输入在获得验证之前都是恶意的。 未做到这一点可能导致应用程序易受攻击。 可能发生的一种类型的攻击称作 SQL 注入，其中恶意代码被添加到字符串中，然后这些字符串被传递到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例中以进行分析和执行。 为了避免这种类型的攻击，应尽可能使用带参数的存储过程，并始终验证用户输入。

在客户端代码中验证用户输入是非常重要的，这样，您就无需浪费时间往返服务器。 在服务器上验证存储过程的参数以捕获无效的和跳过客户端验证的输入，这同样非常重要。

有关 SQL 注入和如何避免此攻击的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“SQL 注入”。 有关验证存储过程参数的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“存储过程 ([!INCLUDE[ssDE](../../includes/ssde_md.md)])”和从属主题。

## <a name="see-also"></a>另请参阅

[保护 JDBC 驱动程序应用程序](../../connect/jdbc/securing-jdbc-driver-applications.md)
