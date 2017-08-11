---
title: "承载 SQL Server 故障转移群集中的报表服务器数据库 |Microsoft 文档"
ms.custom: 
ms.date: 03/30/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7bd5f019-2857-452f-a023-cc3b9e93aec4
caps.latest.revision: 5
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b14768db398059289f280ca610c8b93ca95c468f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="host-a-report-server-database-in-a-sql-server-failover-cluster"></a>在 SQL Server 故障转移群集中承载报表服务器数据库
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供了故障转移群集的支持，以便你可以使用多个磁盘的一个或多[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。 对故障转移群集的支持仅限于报表服务器数据库；您不能将报表服务器服务作为故障转移群集的一部分运行。  
  
 若要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集上承载报表服务器数据库，必须已安装并配置了群集。 然后，当您在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置工具的“数据库安装”页中创建报表服务器数据库时，可以选择该故障转移群集作为服务器名称。  
  
 尽管报表服务器服务不能参与故障转移群集，但是您可以在装有 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 故障转移群集的计算机中安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 报表服务器的运行独立于故障转移群集。 如果在作为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移实例一部分的计算机上安装了报表服务器，则不需要将故障转移群集用于报表服务器数据库；可以使用不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例来承载该数据库。  
  
## <a name="see-also"></a>另请参阅  
 [报表服务器数据库 &#40;SSRS 本机模式 &#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
 [创建报表服务器数据库 &#40;SSRS 配置管理器 &#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)  
  
  

