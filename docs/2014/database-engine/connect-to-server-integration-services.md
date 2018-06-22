---
title: 连接到服务器 (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.connection.login.dtsserver.f1
ms.assetid: 5be897bd-f36c-4c6a-a91a-13d0d016f8b6
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 38102ce976d5b85a89a68c042f926b062cd6338b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013893"
---
# <a name="connect-to-server-integration-services"></a>连接到服务器 (Integration Services)
  连接到 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 时，可使用此对话框查看或指定选项。  
  
## <a name="options"></a>“常规”  
 **服务器类型**  
 从对象资源管理器进行服务器注册时，请选择要连接到何种类型的服务器： [!INCLUDE[ssDE](../includes/ssde-md.md)]、Analysis Services、Reporting Services 或 Integration Services。 对话框的其余部分只显示适用于所选服务器类型的选项。 从“已注册的服务器”注册服务器时，“服务器类型”框是只读的，并且与“已注册的服务器”组件中显示的服务器类型匹配。 若要注册其他类型的服务器，请在开始注册新服务器之前，从“已注册的服务器”工具栏中选择 [!INCLUDE[ssDE](../includes/ssde-md.md)]、Analysis Services、Reporting Services 或 Integration Services。  
  
 **服务器名称**  
 选择要连接到的服务器。 默认情况下，显示上次连接到的服务器实例。  
  
> [!NOTE]  
>  不要使用 *\<servername >*\\*\<instancename >*，这是因为[!INCLUDE[ssIS](../includes/ssis-md.md)]不支持的计算机上的多个实例。  
  
 **身份验证**  
 只有 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 身份验证可用于 [!INCLUDE[ssIS](../includes/ssis-md.md)]。 Windows 身份验证模式允许用户通过 Windows 用户帐户进行连接。  
  
 **用户名**  
 由于只有 Windows 身份验证可用于 [!INCLUDE[ssIS](../includes/ssis-md.md)]，因此此选项不可用。  
  
 **密码**  
 由于只有 Windows 身份验证可用于 [!INCLUDE[ssIS](../includes/ssis-md.md)]，因此此选项不可用。  
  
 **“连接”**  
 单击此项可连接到在上面选择的服务器。  
  
 **选项**  
 单击此项可显示其他服务器连接选项，如注册服务器和记住密码。  
  
  