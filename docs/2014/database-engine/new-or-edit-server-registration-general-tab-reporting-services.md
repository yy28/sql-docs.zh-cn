---
title: 新建或编辑服务器注册 （常规选项卡） (Reporting Services) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.registerserver.general.reportserver.f1
ms.assetid: 5f899a8e-52ef-46b5-b7a9-f200ccd9f724
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 17c10bb36de85a7d0ad1d9522d5d54a540d51a61
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027734"
---
# <a name="new-or-edit-server-registration-general-tab-reporting-services"></a>新建或编辑服务器注册（“常规”选项卡）(Reporting Services)
  在注册 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 实例时，使用此选项卡可以指定选项。  
  
 若要访问此页，请在已注册的服务器中，在“已注册的服务器”工具栏上单击“Reporting Services”，右键单击任意已注册的服务器组（如“Reporting Services”），指向“新建”，再单击“服务器注册”。  
  
## <a name="options"></a>“常规”  
 **服务器类型**  
 从已注册的服务器中注册某服务器时，“服务器类型”框是只读的，它与“已注册的服务器”窗格中显示的服务器类型相匹配。 若要注册其他类型的服务器，请在开始注册新服务器之前，在 **“已注册的服务器”** 工具栏上单击所需的服务器。  
  
 **服务器名称**  
 指定要连接到的报表服务器实例。 在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]中，可以通过报表服务器的实例名访问该服务器。 您安装的每个 SQL Server 实例都可以有一个报表服务器实例。 如果使用默认实例，请键入 SQL Server 实例的名称。 如果使用命名实例，请以 MSSQL$InstanceName 格式指定要连接到报表服务器的命名实例。  
  
 **身份验证**  
 连接到报表服务器时进行的身份验证是通过 Internet 信息服务 (IIS) 完成的。 请从以下身份验证模式中选择一个，以便在连接到 Reporting Services 时使用：  
  
 **Windows 身份验证模式（Windows 身份验证）**  
 使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 凭据连接到报表服务器实例。  
  
 **基本身份验证**  
 如果将 Reporting Services 安装配置为使用基本身份验证，则使用“基本身份验证”进行连接。  
  
 **窗体身份验证**  
 如果将 Reporting Services 安装配置为使用自定义身份验证扩展插件，则使用“窗体身份验证”进行连接。  
  
 **用户名**  
 输入用于连接的登录名。 只有在选择了 **“基本身份验证”** 或 **“窗体身份验证”** 时，此选项才可用。  
  
 **密码**  
 输入用户名的密码。 只有在选择了 **“基本身份验证”** 或 **“窗体身份验证”** 时，此选项才可编辑。  
  
 **记住密码**  
 存储已经输入的密码。 只有在单击了 **“基本身份验证”** 或 **“窗体身份验证”** 时，此选项才可用。  
  
> [!NOTE]  
>  如果已经存储了此密码，而现在要放弃存储，请清除此复选框，再单击“保存”。  
  
 **已注册的服务器名称**  
 希望在“已注册的服务器”中显示的名称。 此名称不必与 **“服务器名称”** 框中的名称相匹配。  
  
 **已注册的服务器说明**  
 输入服务器的说明（可选）。  
  
 **测试**  
 单击此项可测试与“服务器名称”中所选服务器的连接。  
  
 **保存**  
 单击此项可保存已注册服务器的设置。  
  
  