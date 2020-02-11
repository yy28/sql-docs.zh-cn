---
title: 接受许可条款 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- license terms
helpviewer_keywords:
- Registration Information page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Registration Information page
ms.assetid: 08dd739d-5817-4418-bcff-74ab7f8bbd33
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 99418b11eecdb3077e3def746eae56e43bab2d60
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66096841"
---
# <a name="accept-license-terms"></a>接受许可条款
  使用 **安装向导的** “接受许可条款” [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 页可以接受该 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本的许可条款。  
  
 您可以打印许可协议或将其复制到剪贴板。 若要继续，请接受许可条款，然后单击 **“下一步”**。 若要关闭安装过程，请单击 **“取消”**。  
  
## <a name="customer-experience-improvement-program-ceip"></a>客户体验改善计划 (CEIP)  
 如果启用 CEIP 报告，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将被配置为定期向 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 发送报告。 报告将包含有关硬件配置和用户如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和组件的信息。 
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 将使用功能使用情况数据来改进 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 此功能监视的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件包括以下各项：  
  
-   
  [!INCLUDE[ssDE](../../includes/ssde-md.md)]
  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   复制  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]程序  
  
 有关功能使用情况的信息将发送到 [!INCLUDE[msCoName](../../includes/msconame-md.md)]，在那里保存这些信息，且其访问将受到限制。  
  
 若要在安装程序完成后禁用 CEIP 报告，请使用 "**配置工具**" 菜单[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上的 " ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]错误和使用情况报告**" 工具。  
  
 对于诸如安装、升级、修复等此类安装程序操作，仅在执行安装程序期间才收集和上载信息。  
  
 对于所有其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件，将每天针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的所有已启用实例收集一次信息。 收集时间默认为在午夜，以便最大程度上减小服务器的负载。 如果要更改收集时间，可以手动编辑控制收集时间的注册表项。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的各个实例有自己的注册表项：  
  
 \\[!INCLUDE[msCoName](../../includes/msconame-md.md)]HKLM\Software\\\MSSQL12.[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\<INSTANCEID> \cpe\timeofreporting  
  
 该注册表项的值包含运行收集的时间，以从 00:00（午夜）起的分钟数计。 例如，值为 60 会在凌晨 1:00 运行收集，而值为 1200 会在晚上 8:00 运行收集，等等。  
  
## <a name="error-reporting"></a>错误报告  
 使用 **安装向导的** “错误和使用情况报告设置” [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 页，可以启用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的功能错误和使用情况报告功能。  
  
### <a name="options"></a>选项  
 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]及其组件，功能使用情况数据收集和错误报告功能在默认情况下已禁用。  
  
 错误报告  
 如果启用错误报告功能， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将配置为在下列任意 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 组件中发生错误时，自动发送报告到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ：  
  
-   
  [!INCLUDE[ssDE](../../includes/ssde-md.md)]
  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理商  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   复制  
  
 
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 利用错误报告来改进 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的功能，并且对所有信息保密。  
  
 有关错误的信息将通过安全 (https) 连接发送到 [!INCLUDE[msCoName](../../includes/msconame-md.md)]，在那里保存这些信息，且对其访问将受到限制。 另外，也可以将这些信息发送到您自己的“公司错误报告”服务器。  
  
 错误报告包含下列信息：  
  
-   发生问题时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的状态。  
  
-   操作系统版本和计算机硬件信息。  
  
-   用户数字产品 ID（并非用于标识您的许可证）。  
  
-   计算机或代理服务器的网络 IP 地址。  
  
-   来自出错进程的内存或文件的信息。  
  
 
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 无意收集您的文件、姓名、地址、电子邮件地址或任何其他私人信息。 但是，错误报告可能包含来自导致错误的进程的内存或文件中的个人信息。 虽然使用这些信息有可能确定您的身份，但 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 不会将这些信息用于此目的。  
  
 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 隐私保护和数据收集策略的详细信息，请参阅 [Microsoft SQL Server 隐私声明](../../../2014/getting-started/microsoft-sql-server-privacy-statement.md)。  
  
 如果启用了错误报告功能并出现错误，则 Windows 事件日志中可能会包含来自 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 的一条响应，该响应指向与特定错误有关的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知识库文章。  
  
 若要在安装程序完成后禁用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 及其组件的所有实例的错误或功能使用情况报告，请转到 **“错误和使用情况报告设置”** 对话框并清除 **“功能使用情况”** 的复选框。 如果为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的多个[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]组件（、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和共享组件）启用了**错误报告**，则可以对单个组件的每个实例以及共享组件（作为**其他**组件列出）禁用错误报告。  
  
## <a name="see-also"></a>另请参阅  
 [关于 SQL Server 许可条款](../../../2014/getting-started/about-the-sql-server-license-terms.md)  
  
  
