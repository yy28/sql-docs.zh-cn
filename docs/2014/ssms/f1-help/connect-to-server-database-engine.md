---
title: 连接到服务器（数据库引擎）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connectoserverunknownservertype.f1
- sql12.swb.connection.login.sqlserver.f1
- sql12.swb.connection.login.sqlce.f1
- sql12.swb.manageSS2k.f1
- sql12.swb.connecttoce.f1
- sql12.swb.connecttoce.connectionproperties.f1
ms.assetid: ee9017b4-8a19-4360-9003-9e6484082d41
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 50a593c625fe50e5d7a1dfbebc40222ac13433c2
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43808273"
---
# <a name="connect-to-server-database-engine"></a>连接到服务器（数据库引擎）
  连接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 时，可使用此对话框查看或指定选项。 大多数情况下，可以通过在“服务器名称”框中输入数据库服务器的计算机名称并单击“连接”来进行连接。 如果要连接到 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]，请使用后面跟有 **\sqlexpress** 的计算机名称。  
  
 许多因素都会对您能否连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]产生影响。  
  
## <a name="options"></a>选项  
 **服务器类型**  
 从对象资源管理器注册服务器时，请选择要连接到的服务器的类型： [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]或 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。 对话框的其余部分只显示适用于所选服务器类型的选项。 从“已注册的服务器”注册某服务器时，“服务器类型”框是只读的，并且与“已注册的服务器”组件中显示的服务器类型匹配。 若要注册其他类型的服务器，请在开始注册新服务器之前，从“已注册的服务器”工具栏中选择“ [!INCLUDE[ssDE](../../includes/ssde-md.md)]”、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、 [!INCLUDE[ssEW](../../includes/ssew-md.md)]或 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 。  
  
 **服务器名称**  
 选择要连接到的服务器实例。 默认情况下，显示上次连接到的服务器实例。  
  
> [!NOTE]  
>  若要连接到 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 的活动用户实例，请使用指定管道名称的 Named Pipes 协议进行连接，例如：np:\\\\.\pipe\3C3DF6B1-2262-47\tsql\query。有关详细信息，请参阅 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 文档。  
  
 **身份验证**  
 连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例时，有两种可用的身份验证模式。  
  
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
  
 **“连接”**  
 单击此项可连接到在上面选择的服务器。  
  
 **选项**  
 单击此项可显示其他服务器连接选项，如注册服务器和记住密码。  
  
  
