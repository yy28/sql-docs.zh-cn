---
title: 如何：运行升级顾问分析向导 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Analysis Wizard
ms.assetid: d7d2a1e2-1179-4c05-9b0f-555b04dd1199
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8481a6d3e6d7e07753cecb2ce2ff91ea626a4dfe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68811097"
---
# <a name="how-to-run-the-upgrade-advisor-analysis-wizard"></a>如何运行升级顾问分析向导
  可以从升级顾问起始页启动升级顾问分析向导。 本主题介绍了如何运行升级顾问分析向导。  
  
> [!IMPORTANT]
>  运行升级顾问分析向导时，升级顾问会将报表保存在默认报表文件夹中。 但是，报表查看器只显示最近保存的五个报表。 报表的默认位置为 "我的文档\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] " 升级 advisor\110\reports。  
  
### <a name="to-run-the-upgrade-advisor-analysis-wizard"></a>运行升级顾问分析向导  
  
1.  在升级顾问起始页上，单击 "**启动升级顾问分析向导**"。  
  
2.  在 " ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]组件**" 页上，在 "**服务器名称**" 框中输入要扫描的服务器的名称，然后单击 "**检测**"。 输入服务器名称时应遵守以下原则：  
  
    -   若要扫描非群集实例，请输入计算机名。  
  
    -   若要扫描群集实例，请输入虚拟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名称。  
  
    -   若要扫描安装在群集节点上的非群集组件，请输入节点名称。  
  
    > [!WARNING]  
    >  升级顾问不支持到未设置为使用标准端口 (1433) 进行客户端连接的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的连接。 如果要连接到不使用标准端口 (1433) 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请使用 IP 地址和端口创建一个别名。 有关为实例配置客户端协议和创建别名的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]详细信息，请参阅[配置客户端协议](../../database-engine/configure-windows/configure-client-protocols.md)。  
    >   
    >  如果在运行升级顾问[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的计算机上未安装，请单击 "**开始**"，然后单击 "运行`cliconfg`"。 这将打开 " ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端网络实用工具**" 对话框。 使用 "**别名**" 选项卡创建别名。  
  
3.  查看检测到的组件列表，根据需要修改所选内容，然后单击 "**下一步**"。  
  
4.  在 "**连接参数**" 页上，选择要[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]扫描的实例，选择身份验证方法，并在必要时输入用户名和密码信息，然后单击 "**下一步**"。  
  
     默认实例名为 MSSQLSERVER。  
  
5.  对于选定的组件，请输入所需的信息。 有关各个对话框的详细信息，请参阅[升级顾问用户界面参考](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)。  
  
6.  在 "**确认升级顾问设置**" 页上，查看您输入的信息。 如果要提交升级报表，可以选择 "**将报表发送到[!INCLUDE[msCoName](../../includes/msconame-md.md)] ** "。 还可以查看隐私策略。  
  
7.  单击 "**运行**" 以分析的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。  
  
8.  分析完成后，单击 "**启动报告**" 以查看检测到的升级问题。  
  
## <a name="see-also"></a>另请参阅  
 [如何启动升级顾问](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [&#40;用户界面运行升级顾问&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)   
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
