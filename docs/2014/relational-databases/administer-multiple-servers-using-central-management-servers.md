---
title: 使用中央管理服务器管理多个服务器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- multiserver queries
- central management server
- multiserver administration [SQL Server]
- master servers [SQL Server], central management servers
- target configuration [SQL Server]
- server configuration [SQL Server]
ms.assetid: 427911a7-57d4-4542-8846-47c3267a5d9c
caps.latest.revision: 25
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bb33b06555e5804b58bb39b5d02cce349cb8b7c6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37279623"
---
# <a name="administer-multiple-servers-using-central-management-servers"></a>使用中央管理服务器管理多台服务器
  您可以通过指定中央管理服务器并创建服务器组来管理多台服务器。  
  
## <a name="benefits-of-central-management-servers-and-server-groups"></a>中央管理服务器和服务器组的优点  
 指定为中央管理服务器的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例维护服务器组，这些组包含一个或多个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的连接信息。 可以对服务器组同时执行 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句和基于策略的管理策略。 还可以查看通过中央管理服务器管理的实例上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 日志文件。 不能将早于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本的 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 指定为中央管理服务器。  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句。  
  
### <a name="related-tasks"></a>Related Tasks  
 若要创建中央管理服务器和服务器组，请使用 **中的** “已注册的服务器” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]窗口。 请注意，中央管理服务器不能是它所维护的组的成员。 有关如何创建中央管理服务器和服务器组的详细信息，请参阅[创建中央管理服务器和服务器组 (SQL Server Management Studio)](../ssms/register-servers/create-a-central-management-server-and-server-group.md)。  
  
## <a name="see-also"></a>请参阅  
 [使用基于策略的管理来管理服务器](policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
