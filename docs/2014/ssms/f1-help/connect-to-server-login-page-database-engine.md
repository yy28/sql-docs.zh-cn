---
title: 连接到服务器（“登录”页）数据库引擎 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttosqlserver.login.f1
ms.assetid: e08cfbc3-bed5-4401-a13b-1c66d902fe32
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b7f8c761a052bc3c82789087bb955c760e9a1b49
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37181234"
---
# <a name="connect-to-server-login-page-database-engine"></a>连接到服务器（“登录”页）数据库引擎
  连接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 时，使用此选项卡可查看或指定选项。  
  
> [!NOTE]  
>  若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证进行连接，必须在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证和 Windows 身份验证模式下配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 有关如何确定身份验证模式，以及如何更改身份验证模式的详细信息，请参阅[更改服务器身份验证模式](../../database-engine/configure-windows/change-server-authentication-mode.md)。  
  
## <a name="options"></a>“常规”  
 **服务器类型**  
 从对象资源管理器进行服务器注册时，请选择要连接到何种类型的服务器： [!INCLUDE[ssDE](../../includes/ssde-md.md)]、Analysis Services、Reporting Services 或 Integration Services。 对话框的其余部分只显示适用于所选服务器类型的选项。 从“已注册的服务器”注册某服务器时，“服务器类型”框是只读的，并且与“已注册的服务器”组件中显示的服务器类型匹配。 若要注册其他类型的服务器，请在开始注册新服务器之前，从“已注册的服务器”工具栏中选择[!INCLUDE[ssDE](../../includes/ssde-md.md)]、Analysis Services、Reporting Services 或 Integration Services。  
  
 在通过 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库引擎的一个实例时，必须使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，并且必须在“连接到服务器”对话框的“连接属性”选项卡上指定一个数据库。请确保选中“加密连接”复选框。  
  
 默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将连接到 **master**。 如果您指定一个用户数据库，在对象资源管理器中将只会看到该数据库及其对象。 如果连接到 **master**，可以看到所有数据库。 有关详细信息，请参阅 [Windows Azure SQL 数据库概述](http://go.microsoft.com/fwlink/?LinkId=163948)。  
  
 **服务器名称**  
 选择要连接到的服务器实例。 默认情况下，显示上次连接到的服务器实例。  
  
 **身份验证**  
 在连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例时，可以使用两种身份验证模式。  
  
 在通过 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库引擎的一个实例时，必须使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，并且必须在“连接到服务器”对话框的“连接属性”选项卡上指定一个数据库。请确保选中“加密连接”复选框。  
  
 默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将连接到 **master**。 如果您指定一个用户数据库，在对象资源管理器中将只会看到该数据库及其对象。 如果连接到 **master**，可以看到所有数据库。 有关详细信息，请参阅 [Windows Azure SQL 数据库概述](http://go.microsoft.com/fwlink/?LinkId=163948)。  
  
 **Windows 身份验证模式（Windows 身份验证）**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 身份验证模式允许用户通过 Windows 用户帐户进行连接。  
  
 **SQL Server 身份验证**  
 当用户使用指定的登录名和密码从不可信连接进行连接时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将通过检查是否已设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户以及指定的密码是否与以前记录的密码匹配，自行进行身份验证。 如果未设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户，则身份验证失败，并且用户会收到一条错误消息。  
  
> [!IMPORTANT]  
>  请尽可能使用 Windows 身份验证。  
  
 **用户名**  
 输入连接所使用的用户名。 只有在已选择使用 Windows 身份验证进行连接的情况下，此选项才可用。  
  
 **登录**  
 输入连接所用的登录名。 只有选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证进行连接时，此选项才可用。  
  
 **密码**  
 输入登录名的密码。 只有在已选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证进行连接的情况下，此选项才可用。  
  
 **记住密码**  
 单击此项可使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存储您所输入的密码。 只有在已选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证进行连接时，才会显示此选项。  
  
 **Connect**  
 单击此项可连接到在上面选择的服务器。  
  
 **选项**  
 单击此选项更改对话框并隐藏其他服务器连接选项，例如记住密码。  
  
  
