---
title: “连接属性”对话框 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connectionproperties.f1
helpviewer_keywords:
- Connection Properties dialog box
ms.assetid: 6df812ad-4d80-4503-8a23-47719ce85624
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 80e858e75cec96b7e56e16fa7465a22048563726
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934599"
---
# <a name="connection-properties-dialog-box"></a>“连接属性”对话框
  使用此对话框可以查看当前的连接属性。 在不同“对象资源管理器”对话框中单击“查看连接属性”**** 时，可以使用此对话框。 此页上显示的属性是只读的。  
  
 若要更改属性（如“数据库”****），请在打开“连接属性”**** 对话框之前，使用“对象资源管理器”连接到所需的数据库。  
  
 请注意，SQL Azure 的查询超时期限是 30 分钟。  
  
## <a name="authentication"></a>身份验证  
 查看当前连接的身份验证属性。 身份验证属性是指在建立连接时所使用的登录名和身份验证方法。 若要更改身份验证属性，请断开与的连接， [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 然后使用所需的连接选项将对象资源管理器再次连接到服务器。  
  
 **身份验证方法**  
 用于当前连接的身份验证方法。  
  
 **用户名**  
 用于连接身份验证的登录的用户名。  
  
## <a name="connection-category"></a>连接类别  
 查看当前连接的连接属性。 大多数连接属性都是在连接过程中，在“连接到服务器”**** 对话框的“连接属性”**** 选项卡上选择的。  
  
 **Database**  
 当前连接到的数据库的名称。 若要更改此名称，请使用 SQL 编辑器工具栏。  
  
 **SPID**  
 服务器为连接所分配的系统进程 ID。 不能更改此连接的 SPID。  
  
 **网络协议**  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 连接的网络协议。 若要对此进行更改，请使用所需的连接属性再次连接。  
  
 **网络数据包大小**  
 与服务器通信时所使用的数据包的大小。 若要对此进行更改，请使用所需的连接属性再次连接。  
  
 **连接超时**  
 连接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 时，在发生超时并向用户返回连接失败错误之前等待的时间（秒）。 若要对此进行更改，请使用所需的连接属性再次连接。  
  
 **执行超时**  
 在服务器上完成任务执行之前等待的时间（秒）。 若要对此进行更改，请使用所需的连接属性再次连接。  
  
 **加密**  
 当前的连接是否经过加密。 若要对此进行更改，请使用所需的连接属性再次连接。  
  
## <a name="product-category"></a>产品类别  
 查看当前连接的产品属性。 这些属性描述服务器产品、版本、实例名和排序规则。 这些属性在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安装过程中进行设置。  
  
 **产品名称**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的产品名称。  
  
 **产品版本**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的产品版本。  
  
 **服务器名称**  
 运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的计算机的名称。  
  
 **Instance Name**  
 服务器的实例名称。 默认实例为空白。  
  
 **语言**  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 产品的语言版本。  
  
 **排序规则**  
 服务器的排序规则。  
  
## <a name="server-environment-category"></a>服务器环境类别  
 查看当前连接与服务器硬件和操作系统相关的服务器环境属性。 这些属性不能使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]进行配置。  
  
 **计算机名称**  
 运行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的服务器计算机的名称。  
  
 **平台**  
 服务器的操作系统名称、制造商名称和 CPU 系列。  
  
 **操作系统**  
 服务器上安装的 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 的版本。  
  
 **Processors**  
 服务器上处理器的数量。  
  
 **Operating System Memory**  
 服务器上物理内存的总量 (MB)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Management Studio 中的属性页](../ssms/property-pages-in-sql-server-management-studio.md)   
 [连接到服务器（“登录”页）数据库引擎](../ssms/f1-help/connect-to-server-login-page-database-engine.md)  
  
  
