---
title: SMO 对象模型 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- object models [SMO]
- SMO [SQL Server], object model
- SQL Server Management Objects, object model
ms.assetid: bd6e59b6-ca46-42c0-adb2-c9d64cf6e00b
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: bbaf5430252c296313723509b0195cdf5573ced5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017045"
---
# <a name="smo-object-model"></a>SMO 对象模型
  SMO 对象模型由对象的层次结构构成。 <xref:Microsoft.SqlServer.Management.Smo.Server> 对象是顶层对象，所有实例类对象都位于 <xref:Microsoft.SqlServer.Management.Smo.Server> 对象之下。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 类是具有单独的对象层次结构的顶级类。 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer>对象所表示[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服务和网络设置可通过 WMI 提供程序。  
  
 除了 <xref:Microsoft.SqlServer.Management.Smo.Server> 和 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 对象外，存在若干表示任务或操作的实用工具类，例如 <xref:Microsoft.SqlServer.Management.Smo.Transfer>、<xref:Microsoft.SqlServer.Management.Smo.Backup> 或 <xref:Microsoft.SqlServer.Management.Smo.Restore>。  
  
 SMO 对象模型由若干命名空间构成。 有关详细信息，请参阅 [SMO 命名空间](smo-object-model-namespaces.md)。  
  
## <a name="see-also"></a>请参阅  
 [SMO Object Model Diagram](smo-object-model-diagram.md)   
 [SMO 命名空间](smo-object-model-namespaces.md)   
 [用于配置管理的 WMI 提供程序的概念](../wmi-provider-configuration/wmi-provider-for-configuration-management.md)  
  
  