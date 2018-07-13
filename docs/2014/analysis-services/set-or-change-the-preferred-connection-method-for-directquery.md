---
title: 设置或更改 DirectQuery 的首选的连接方法 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f10d5678-d678-4251-8cce-4e30cfe15751
caps.latest.revision: 5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c5c9ad99aad3ae46b3e97c3d3b6dfbec03dcff27
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37149518"
---
# <a name="set-or-change-the-preferred-connection-method-for-directquery"></a>设置或更改 DirectQuery 的首选连接方法
  当您创建在 DirectQuery 模式下使用的模型时，必须首先对设计环境进行配置以便支持使用 DirectQuery。 若要执行此操作，请参阅[启用 DirectQuery 设计模式&#40;SSAS 表格&#41;](tabular-models/enable-directquery-mode-in-ssdt.md)。  
  
 在您做好部署模型的准备后，必须设置其他一些属性以使用户能够使用某一 DirectQuery 模式访问您的模型：  
  
-   您必须指示针对模型的查询是应该使用缓存数据还是关系数据源。 您只能使用混合模式或 DirectQuery。  
  
-   如果您正在使用分区，则必须指示哪一分区用作 DirectQuery 数据源。  
  
-   您必须为将访问 SQL Server 数据源的用户设置模拟选项。  
  
 此过程介绍如何在设计器中为 DirectQuery 模型设置首选连接方法。 还介绍了在部署了模型后，如何在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中更改此属性。  
  
### <a name="to-set-the-preferred-connection-method-for-a-directquery-model"></a>为 DirectQuery 模型设置首选连接方法  
  
1.  在[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，打开 DirectQuery 模型的解决方案文件。  
  
2.  在 Visual Studio 中，从 **“项目”** 菜单中，选择 **“属性”**。  
  
3.  在 **“属性”** 窗格中，将属性 **DirectQueryMode**更改为支持 DirectQuery 使用的以下值之一：  
  
    -   **InMemory 以及 DirectQuery**：如果您使用此选项，则部署模型，但您必须首先处理缓存，然后才能对模型运行查询。  
  
    -   **DirectQuery 以及 InMemory**：如果您使用此选项，则缓存将可供客户端使用（如果已处理缓存）。 如果您使用此设置部署模型并且未处理缓存，则某些客户端在尝试连接到模型时势必会收到错误消息。  
  
    -   **仅限 DirectQuery**：如果您使用此选项，则部署元数据，但模型对其中的数据没有影响。 尝试使用内存中模式进行连接的客户端将会收到错误消息，指示模型不存在或尚未处理。  
  
4.  如果存在错误，则在 Visual Studio 中，打开 **“错误列表”** ，并且解决将阻止模型部署在 DirectQuery 模式下的任何问题。  
  
### <a name="to-verify-or-change-the-preferred-connection-method-for-a-directquery-model"></a>为 DirectQuery 模型验证或更改首选连接方法  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中，连接到部署了 DirectQuery 模型的实例。  
  
2.  右键单击该模型数据库并选择 **“属性”**。  
  
3.  在 **“属性”** 窗格中，将属性 **DirectQueryMode**更改为以下值之一：  
  
    -   **仅限 DirectQuery**  
  
    -   **InMemory 以及 DirectQuery**  
  
    -   **DirectQuery 以及 InMemory**  
  
 请注意，这些属性与您在 Visual Studio 中部署前对项目设置的属性相同。 您可以随时更改针对 DirectQuery 模式的首选连接模式，只要您已将模型配置为支持使用 DirectQuery。  
  
## <a name="see-also"></a>请参阅  
 [DirectQuery 模式（SSAS 表格）](tabular-models/directquery-mode-ssas-tabular.md)   
 [启用 DirectQuery 设计模式&#40;SSAS 表格&#41;](tabular-models/enable-directquery-mode-in-ssdt.md)  
  
  
