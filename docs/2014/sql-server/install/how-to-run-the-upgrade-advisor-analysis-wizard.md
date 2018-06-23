---
title: 如何： 运行升级顾问分析向导 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Upgrade Advisor Analysis Wizard
ms.assetid: d7d2a1e2-1179-4c05-9b0f-555b04dd1199
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5ff92f0bb0cbf15e61895307d799415639a89eab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128249"
---
# <a name="how-to-run-the-upgrade-advisor-analysis-wizard"></a>如何运行升级顾问分析向导
  可以从升级顾问起始页启动升级顾问分析向导。 本主题介绍了如何运行升级顾问分析向导。  
  
> [!IMPORTANT]  
>  运行升级顾问分析向导时，升级顾问会将报表保存在默认报表文件夹中。 但是，报表查看器只显示最近保存的五个报表。 报表的默认位置是我的文档\\[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]升级 Advisor\110\Reports。  
  
### <a name="to-run-the-upgrade-advisor-analysis-wizard"></a>若要运行升级顾问分析向导  
  
1.  在升级顾问开始页上，单击**启动升级顾问分析向导**。  
  
2.  上**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]组件**页上，输入要扫描中的服务器名称**服务器名称**框中，并依次**检测**。 输入服务器名称时应遵守以下原则：  
  
    -   若要扫描非群集实例，请输入计算机名称。  
  
    -   若要扫描群集实例，请输入虚拟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名称。  
  
    -   若要扫描安装在群集节点上的非群集组件，请输入节点名称。  
  
    > [!WARNING]  
    >  升级顾问不支持到未设置为使用标准端口 (1433) 进行客户端连接的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的连接。 如果要连接到不使用标准端口 (1433) 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请使用 IP 地址和端口创建一个别名。 有关配置客户端协议以及创建的别名的详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例，请参阅[Configure Client Protocols](../../database-engine/configure-windows/configure-client-protocols.md)。  
    >   
    >  如果你没有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装在运行升级顾问的计算机上，单击**启动**，然后运行`cliconfg`。 这将打开**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端网络实用工具**对话框。 使用**别名**选项卡可以创建别名。  
  
3.  查看检测到的组件的列表，如有必要，修改所做的选择，然后单击**下一步**。  
  
4.  上**连接参数**页上，选择的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]你想要扫描，选择身份验证方法，并如有必要，输入用户名和密码信息，然后单击**下一步**.  
  
     默认实例名为 MSSQLSERVER。  
  
5.  对于选定的组件，请输入所需的信息。 有关各个对话框的详细信息，请参阅[升级顾问用户界面参考](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)。  
  
6.  上**确认升级顾问设置**页上，查看你输入的信息。 你可以选择**将报告发送给[!INCLUDE[msCoName](../../includes/msconame-md.md)]** 如果你想要提交升级报表。 还可以查看隐私策略。  
  
7.  单击**运行**分析的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
8.  完成分析后，单击**启动报表**查看检测到的升级问题。  
  
## <a name="see-also"></a>请参阅  
 [如何： 启动升级顾问](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [运行升级顾问&#40;用户界面&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)   
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  