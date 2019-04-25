---
title: 服务器组中注册 Analysis Services 实例 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 5fd3826b-8f75-48eb-910c-bf784163e53b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9552bd8fac2012ead7359f38776d368b85e0dbd2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62730107"
---
# <a name="register-an-analysis-services-instance-in-a-server-group"></a>在服务器组中注册 Analysis Services 实例
  如果有大量 Analysis Services 服务器实例，可以在 Management Studio 中创建服务器组来方便管理服务器。 服务器组的作用是在管理工作区内提供一组相关服务器的近似性。 例如，假定您负责管理 10 个单独的 Analysis Services 实例。 通过按服务器模式、运行时间条件或部门/区域将它们分组，您可以更易于查看并连接到共享相同特征的实例。 您还可以添加描述性信息，帮助您记住如何使用服务器。  
  
 ![包含成员服务器的已注册服务器窗格](../media/ssas-ssms-registerserver.gif "包含成员服务器的已注册的服务器窗格")  
  
 可以在层次结构中创建服务器组。 本地服务器组是根节点。 它始终包含在本地计算机上运行的 Analysis Services 实例。 您可以将远程服务器添加到任何组，包括本地组。  
  
 创建服务器组后，必须使用“已注册的服务器”窗格查看和连接到成员服务器。 该窗格按服务器类型筛选 SQL Server 实例（数据库引擎、Analysis Services、Reporting Services 和 Integration Services）。 单击某一服务器类型可以查看为它创建的服务器组。 若要连接到组中的特定服务器，可以双击组中的该服务器。  
  
 为服务器定义的连接信息（包括服务器名称）通过服务器注册已持久化。 使用其他工具连接到服务器时，不能修改连接信息或使用注册的名称。  
  
## <a name="create-a-server-group-and-add-registered-servers"></a>创建服务器组并添加已注册的服务器  
  
1.  在 Management Studio 中，单击“查看”菜单中的“已注册的服务器”以在工作区中打开“已注册的服务器”窗格。 默认情况下，已创建本地服务器组。 在本地服务器上运行的所有 Analysis Services 实例是其成员。  
  
2.  右键单击“本地服务器组”，选择“新建服务器组”并指定该组的名称。  
  
3.  右键单击该服务器组，然后选择“新建服务器注册”。 输入本地或远程服务器的网络名称，包括实例名称（如果服务器作为命名实例安装）。 或者，您可以提供在“已注册的服务器”中显示的已注册的服务器名称。 此名称仅在“已注册的服务器”中使用。 您不能使用它来重命名服务器，也不能在连接字符串中使用它。 已注册的服务器名称可以比实际服务器名称更具描述性，或包括其他有助于区分此服务器与其他服务器的标识特征。  
  
  
