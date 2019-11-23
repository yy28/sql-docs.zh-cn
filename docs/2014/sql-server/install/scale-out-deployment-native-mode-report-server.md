---
title: 扩展部署（本机模式报表服务器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.scaleoutdeployment.F1
ms.assetid: 4df38294-6f9d-4b40-9f03-1f01c1f0700c
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: a9fe82102df73ddfa77b4636dd29793ac2694949
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952418"
---
# <a name="scale-out-deployment-native-mode-report-server"></a>扩展部署（本机模式报表服务器）
  使用 **配置管理器中的** “扩展部署” [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 页可以查看扩展部署的初始化状态或将报表服务器联接到扩展部署。 “扩展部署” 是指共享单个报表服务器数据库的两个或多个报表服务器实例。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式。  
  
 “已初始化的报表服务器” 是指可以对报表服务器数据库中存储的敏感数据进行加密和解密的服务器（已存储凭据和连接字符串是存储在此数据库中的加密数据示例）。 报表服务器初始化是一项必需的报表服务器操作。  
  
 在以下情形中使用“扩展部署” ：  
  
-   作为对服务器群集中的多个报表服务器进行负载平衡的必备条件。 在可以对多个报表服务器进行负载平衡之前，必须首先将它们配置为共享同一报表服务器数据库。  
  
-   通过使用一个服务器处理交互式报表同时使用另一个服务器处理计划的报表，将报表服务器应用程序分段置于不同的计算机上。 在此情况下，每个服务器实例均按照共享报表服务器数据库中存储的同一报表服务器内容来处理不同类型的请求。  
  
 若要配置扩展部署，则首先应有两个或多个与同一报表服务器数据库连接的报表服务器实例。 安装所有实例后，连接到第一个报表服务器，然后使用“扩展部署”页联接每个附加实例。 只有已初始化为使用数据库的报表服务器才能初始化其他节点。  
  
 若要打开此页，请启动 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置管理器，然后在导航窗格中选择 **“扩展部署”** 。 有关详细信息，请参阅 [Reporting Services Configuration Manager（本机模式）](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)。  
  
## <a name="options"></a>“常规”  
 **SQL Server 名称**  
 指定承载报表服务器数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例的名称。  
  
 **Database Name**  
 指定报表服务器实例当前连接到的数据库的名称。  
  
 **服务器模式**  
 显示服务器和数据库的模式。 服务器模式为“本机”或“SharePoint 集成”。 这两种模式均支持扩展部署。  
  
 **“服务器”**  
 显示报表服务器名称。 在大多数情况下，此为安装报表服务器的计算机的名称。  
  
 **实例**  
 显示报表服务器实例名称。 报表服务器实例基于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
 **状态**  
 指示报表服务器是已初始化还是正在等待联接扩展部署：  
  
-   对于不属于扩展部署的独立报表服务器，此页说明此报表服务器实例已根据其专用报表服务器数据库进行初始化。 “状态”设置为 **“已联接”** 。  
  
-   对于正在等待联接扩展部署的报表服务器，此页的“服务器”、“实例”和“状态”均为空值。 如果选择的现有报表服务器数据库已由其他报表服务器实例使用，则报表服务器将处于等待联接扩展部署状态。 此页上的消息将指示您连接到已与场联接的报表服务器。 若要完成该请求，请单击 **“连接”** ，选择已初始化为使用报表服务器数据库的报表服务器，接着单击 **“扩展部署”** ，选择状态为 **“正在等待联接”** 的报表服务器实例，然后单击 **“初始化”** 。  
  
-   对于当前作为扩展部署一部分的报表服务器，此页显示共享同一个报表服务器数据库的所有报表服务器实例的初始化状态。 查看扩展部署的状态时，连接到哪个服务器无关紧要。 对扩展部署中的所有节点均以相同的方式报告它们的状态信息。  
  
     对于属于扩展部署的报表服务器，可使用此页来添加或删除节点。  
  
 **初始化**  
 单击 **“初始化”** 可将报表服务器添加到扩展部署中。 该步骤用于将报表服务器配置为使用共享报表服务器数据库中的对称密钥。 可以使用 **“初始化”** 将报表服务器实例添加到扩展部署中，或者排除迁移或安装故障。  
  
 除非您事先配置了与共享报表服务器数据库的连接，否则报表服务器实例将不可用。 此外，还必须从已初始化为使用报表服务器数据库的报表服务器执行初始化操作。  
  
 **删除**  
 单击 **“删除”** 可以从报表服务器数据库中删除选定报表服务器实例的加密密钥。 您可以通过删除密钥将报表服务器从扩展部署中删除，或者排除迁移或安装故障。 使用此选项，将仅删除指定报表服务器实例的加密密钥。 报表服务器数据库中的加密数据不受影响。  
  
 请确保在删除密钥之前创建了该密钥的备份副本，作为一种防范措施。 一旦删除列表中最后一个报表服务器的加密密钥，将对该数据库的任何后续报表服务器初始化提出新的要求。 新的要求是初始化报表服务器之后，必须还原对称密钥的备份副本。 如果希望访问报表服务器数据库中当前存在的加密数据，还原对称密钥是必需的。  
  
 如果不再需要加密数据或者没有密钥的备份副本，则必须删除该加密数据。 有关详细信息，请参阅[加密&#40;密钥 SSRS 本机&#41;模式](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)。  
  
## <a name="see-also"></a>另请参阅  
 [初始化 Report Server（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [配置和管理加密密钥（SSRS 配置管理器）](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)   
 [配置本机模式报表服务器扩展部署（SSRS 配置管理器）](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
  
  
