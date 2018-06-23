---
title: SQL Server 组件 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Upgrade Advisor, components
- listing components to analyze
- Upgrade Advisor [SQL Server], components
- component analysis [Upgrade Advisor]
- finding components to analyze
- locating components to analyze
- detecting components to analyze
- server names [Upgrade Advisor]
- analyzing system [Upgrade Advisor], component list
- identifying components to analyze
ms.assetid: 539b9525-ce3f-4950-9146-5527a5a297ee
caps.latest.revision: 41
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 85a89e2114cd00b28444cf6ee62d12ff1abdec42
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127455"
---
# <a name="sql-server-components"></a>SQL Server 组件
  具有的本地或远程计算机上运行升级顾问分析向导[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]， [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]， [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]，或[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]安装。 升级前分析的第一步是确定要分析的计算机和组件。  
  
## <a name="options"></a>“常规”  
 **计算机名称**  
 指定要分析的计算机的名称。 升级顾问填充**服务器名称**包装盒本地计算机的名称。 也可以使用“.”和“localhost”连接本地计算机。  
  
 若要对其他计算机进行分析，请遵循下列准则：  
  
-   若要扫描非群集实例，请输入计算机名称。  
  
-   若要扫描群集实例，请输入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例的名称。  
  
-   若要扫描安装在群集节点上的非群集组件，请输入故障转移群集节点的计算机名称。  
  
    > [!IMPORTANT]  
    >  切勿包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名。  
  
 可以不指定计算机名称，而指定 IP 地址。  
  
 如果扫描 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，则必须指定本地计算机的名称。 升级顾问仅扫描本地报表服务器。  
  
 **检测**  
 **检测**按钮访问指定的计算机，并检测到组件来分析：  
  
-   如果要分析远程计算机上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，则必须在远程计算机上启用远程注册表服务。  
  
-   如果在计算机的注册表中发现 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 的实例，将检测到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]。  
  
-   如果在计算机的注册表中发现 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，将检测到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
-   如果在计算机的注册表中发现 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]，将检测到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 不过，升级顾问仅扫描本地报表服务器。  
  
 **组件**  
 选择要分析的组件。 你可以单击**检测**按钮以选择所有计算机上安装的组件。 检测为已安装在计算机上的组件旁边会出现一个复选标记。 还可以通过选中或清除各个组件旁边的复选框来手动选择所要分析的组件。  
  
## <a name="see-also"></a>请参阅  
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [升级顾问用户界面参考](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  