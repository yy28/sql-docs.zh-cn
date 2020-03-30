---
title: 启用和禁用“我的报表”| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- deactivated My Reports folder
- folders [Reporting Services], My Reports
- activated My Reports folder
- My Reports folder [Reporting Services]
- disabling My Reports folder
ms.assetid: 16c76e82-9fd4-417c-9ed3-a7d5bcd1dba2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6670d1da918ac1bdc6cb1947b265f9d543259814
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "65577778"
---
# <a name="enable-and-disable-my-reports"></a>启用和禁用“我的报表”
  使用“我的报表”功能可以在报表服务器数据库内分配个人存储区，便于用户在私人文件夹中保存自己的报表。 报表服务器管理员可以启用或禁用此功能，或通过修改控制用户如何使用此工作区的安全设置，来更改该功能的工作方式。  
  
 默认情况下，将禁用“我的报表”功能。 您可以对所有用户启用或禁用该功能，但不能对一部分用户启用该功能。 大多数用户和单位都认为这项功能颇有价值；请权衡本主题下文列出的优缺点，确定该功能是否适用于您的单位。  
  
## <a name="how-to-enable-and-disable-my-reports"></a>如何启用和禁用“我的报表”功能  
 若要使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]启用“我的报表”功能，请连接到报表服务器实例，打开 **“服务器属性”** 页。 然后在 **“常规”** 选项卡上选中 **“为每个用户启用‘我的报表’文件夹”** 选项。  
  
 用于“我的报表”功能的角色定义可确定在“我的报表”工作区中支持哪些操作。 例如，如果“我的报表”角色不包括“创建链接报表”任务，用户将无法在“我的报表”文件夹中创建链接报表。 有关详细信息，请参阅 [保护我的报表](../../reporting-services/security/secure-my-reports.md)。  
  
 若要停用“我的报表”功能，请清除 **“为每个用户启用‘我的报表’文件夹。”** 。 停用“我的报表”功能将为用户移除“我的报表”文件夹的所有可见的指示形式。 一旦禁用该功能，您必须手动删除提供实际存储位置的文件夹（即“用户文件夹”中的子文件夹）。  
  
### <a name="when-my-reports-is-activated"></a>激活“我的报表”功能之后  
 一旦激活该功能，用户将在根文件夹（即“主文件夹”）之下看到“我的报表”文件夹。 除了“我的报表”文件夹外，报表服务器管理员还会在“用户文件夹”文件夹中看到对应每个用户的子文件夹。  
  
 激活该功能后，将无法删除“用户文件夹”及其子文件夹。 此外，名称“我的报表”将成为根节点（主文件夹）下创建的文件夹的保留名称。  
  
 如果在停用“我的报表”功能后激活它，报表服务器将创建新的“用户文件夹”文件夹（如果尚不存在）。 如果“用户文件夹”已存在，报表服务器将在用户登录到各自的“我的报表”文件夹时添加新的子文件夹。  
  
### <a name="when-my-reports-is-deactivated"></a>停用“我的报表”功能之后  
 一旦停用该功能，名称“我的报表”将不再保留；这时用户可以在主文件夹下创建名为“我的报表”的个人文件夹。 此外，不再执行从“我的报表”到用户特定的“我的报表”子文件夹的重定向。 最后，在 URL 地址中包括用户特定“我的报表”文件夹的任何报表链接都将不再有效。  
  
## <a name="choosing-to-use-my-reports"></a>选用“我的报表”功能  
 是否使用“我的报表”功能取决于您是否希望将一些服务器资源专门用于支持用户工作区。 “我的报表”是一项强大的功能，用户可以使用该功能控制协助他们完成工作的信息资源。 通过该功能，用户还可以处理不常用的报表。 使用“我的报表”的一个最主要的原因在于：它为需要编制和查看报表的用户提供了安全、易管理的支持功能。 如果没有此功能，您会发现自己需要专门为各个用户创建文件夹和安全策略。 随着用户和用户需求的变化，这种方式势必造成文件夹和策略的数量不断增加，时间越久越不易维护。  
  
 请注意，如果确实激活了“我的报表”功能，对于单击“我的报表”链接并且具有域帐户的每个用户，即使用户并不希望或不需要“我的报表”文件夹，报表服务器也会为这些用户创建该文件夹。 无法通过系统确定哪些文件夹正在使用。 您必须手动检查各文件夹，确定其中是否包含内容。  
  
## <a name="see-also"></a>另请参阅  
 [保护我的报表](../../reporting-services/security/secure-my-reports.md)   
 [报表服务器内容管理（SSRS 本机模式）](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)  
  
  
