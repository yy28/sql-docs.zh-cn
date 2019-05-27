---
title: 连接参数 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server], connections
- authentication [Upgrade Advisor]
- SQL Server Upgrade Advisor, connections
- connections [Upgrade Advisor]
- server instances [Upgrade Advisor]
- default server instances
- analyzing system [Upgrade Advisor], connections
ms.assetid: f754d038-637a-4d8e-85b0-b242e6499d26
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ca5d6ed8f1e8a92d22bd32e39c8afe946a0fcfee
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66095979"
---
# <a name="connection-parameters"></a>连接参数
  若要分析某些服务器类型（比如 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]），则必须选择具体的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 会自动选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的默认实例。 您可以更改此选择，但一次只能选择一个实例供升级顾问分析。 如果包括了要求身份验证的服务器类型，则必须输入身份验证模式和凭据。  
  
## <a name="options"></a>选项  
 **服务器名称**  
 使用您在“[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件”窗格中输入的计算机名进行预填充。  
  
 **实例名称**  
 从计算机中可用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中进行选择。 如果看不到的实例的列表，请使用 MSSQLSERVER 扫描默认实例。 这对于远程计算机来说尤其重要。 也可以使用单词“default”来扫描默认实例。  
  
 **身份验证**  
 从此计算机上可用的身份验证模式列表中进行选择。 默认情况下，身份验证模式为 Windows 身份验证。  
  
 **用户名**  
 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，请在框中输入用户名。 建议该用户名具有计算机上的管理凭据。  
  
> [!NOTE]  
>  如果选择 Windows 身份验证，在填充当前登录的用户的用户名**用户名**文本框。  
  
 **密码**  
 输入指定用户的密码。  
  
## <a name="see-also"></a>请参阅  
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [升级顾问用户界面参考](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
