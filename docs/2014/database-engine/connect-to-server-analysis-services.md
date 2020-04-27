---
title: 连接到服务器 (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connection.login.analysisserver.f1
ms.assetid: 7e277d22-8d4b-422e-8882-7c5dd7a6d915
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d7dd13f417ccf7b6240d8e3f8328d0b3cd9371bc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62755600"
---
# <a name="connect-to-server-analysis-services"></a>连接到服务器 (Analysis Services)
  连接到 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 时，可以使用此对话框查看或指定选项。  
  
## <a name="options"></a>选项  
 **服务器类型**  
 从对象资源管理器进行服务器注册时，请选择要连接到何种类型的服务器： [!INCLUDE[ssDE](../includes/ssde-md.md)]、Analysis Services、Reporting Services 或 Integration Services。 对话框的其余部分只显示适用于所选服务器类型的选项。 从“已注册的服务器”注册某服务器时，“服务器类型”  框是只读的，并且与“已注册的服务器”组件中显示的服务器类型匹配。 若要注册其他类型的服务器，请在开始注册新服务器之前，从“已注册的服务器”工具栏中选择[!INCLUDE[ssDE](../includes/ssde-md.md)]、Analysis Services、Reporting Services 或 Integration Services。  
  
 **服务器名称**  
 选择要连接到的服务器实例。 默认情况下，显示上次连接到的服务器实例。  
  
 **身份验证**  
 在连接到 Analysis Services 的实例时，支持下列身份验证模式： [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 身份验证。  
  
 **Windows 身份验证模式（Windows 身份验证）**  
 **Windows 身份验证**模式允许用户通过 windows 用户帐户进行连接。  
  
 **用户名**  
 此选项在此版本中不可用。 输入连接所使用的用户名。 仅当已选择使用**Windows 身份验证**进行连接时，此选项才可用。  
  
 **密码**  
 此选项在此版本中不可用。 输入登录名的密码。 只有在已选择使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 身份验证进行连接的情况下，此选项才可用。  
  
 **“连接”**  
 单击此项可连接到在上面选择的服务器。  
  
 **选项**  
 单击此项可显示其他服务器连接选项，如注册服务器和记住密码。  
  
  
