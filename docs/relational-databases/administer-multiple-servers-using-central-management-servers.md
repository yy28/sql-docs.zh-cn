---
title: 使用中央管理服务器管理多台服务器
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- multiserver queries
- central management server
- multiserver administration [SQL Server]
- master servers [SQL Server], central management servers
- target configuration [SQL Server]
- server configuration [SQL Server]
ms.assetid: 427911a7-57d4-4542-8846-47c3267a5d9c
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: a2e2da55bd04ba29cf1c6ef81757488f8d50fd24
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "74055620"
---
# <a name="administer-multiple-servers-using-central-management-servers"></a>使用中央管理服务器管理多台服务器
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  您可以通过指定中央管理服务器并创建服务器组来管理多台服务器。  
  
## <a name="what-is-a-central-management-server-and-server-groups"></a>什么是中央管理服务器和服务器组？  
 指定为中央管理服务器的 SQL Server 实例维护服务器组，这些组包含一个或多个实例的连接信息。 可以对服务器组同时执行 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句和基于策略的管理策略。 还可以查看通过中央管理服务器管理的实例上的日志文件。 
 
 中央管理服务器基本上是包含托管服务器列表的中央存储库。 不能将早于 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 的版本指定为中央管理服务器。  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句。  
  
## <a name="create-central-management-server-and-server-groups"></a>创建中央管理服务器和服务器组 
 若要创建中央管理服务器和服务器组，请使用 **中的** “已注册的服务器” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]窗口。 请注意，中央管理服务器不能是它所维护的组的成员。 
 
 有关如何创建中央管理服务器和服务器组的信息，请参阅[创建中央管理服务器和服务器组 (SQL Server Management Studio)](../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md)。  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来管理服务器](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
