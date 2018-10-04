---
title: 与 SQL Server 的连接（用于删除）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 030b10c2-6b88-4c2c-bf67-22994be25a60
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f347a4866a7b6566ae2f0759813ac99d7977f058
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48143807"
---
# <a name="connection-to-sql-server-for-delete"></a>删除与 SQL Server 的连接
  在不含对 MSXDBCDC 数据库具有写入权限的数据库角色（例如 **db_owner** 角色）的登录名尝试删除某一 Oracle CDC 实例时，“连接到 SQL Server”对话框将显示。  
  
 在此对话框中，你必须为对 MSXDBCDC 数据库具有写入权限的登录名（例如 **db_owner** 数据库角色）输入凭据，以便删除 Oracle CDC 实例。  
  
 在“连接到 SQL Server”对话框中输入以下信息。  
  
 **服务器名称**  
 键入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所在的服务器的名称。  
  
 **身份验证**  
 选择下列选项之一：  
  
-   **Windows 身份验证**  
  
-   **SQL Server 身份验证**：如果选择此选项，则必须在连接到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中为用户键入“登录名”和“密码”。  
  
 **选项**  
 单击箭头可以查看要配置的可用选项。 您可以选择保留这些选项不变，使用其默认值。 可用选项是：  
  
-   **连接超时值**：键入一个时间（秒），未超过该时间，程序将等待建立与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的连接，超过该时间后将生成超时错误。 默认值为 **15**。  
  
-   **执行超时值**：键入一个时间（秒），未超过该时间，程序将等待 SQL 命令执行完成，超过该时间后将生成超时错误。 默认值为 **30**。  
  
-   **加密连接**：选择“加密连接”可确保对正在建立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接进行加密以保护隐私。  
  
-   **高级**：单击“高级”并根据需要在“高级连接属性”对话框中键入任何附加的连接属性。  
  
## <a name="see-also"></a>请参阅  
 [针对 CDC 服务的 SQL Server 连接所需权限](sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
  
