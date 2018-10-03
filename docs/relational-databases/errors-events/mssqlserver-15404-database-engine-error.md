---
title: MSSQLSERVER_15404 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 15404 (Database Engine error)
ms.assetid: 69677f02-bc81-4e4a-99b8-5c1bd1de36df
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 82a28bd2db12d44fa2459cedb691d0043c27ddc3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809555"
---
# <a name="mssqlserver15404"></a>MSSQLSERVER_15404
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|15404|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SEC_NTGRP_ERROR|  
|消息正文|无法获取有关 Windows NT 组/用户“*user*”的信息，错误代码 *code*。|  
  
## <a name="explanation"></a>解释  
在指定无效主体时，15404 用于身份验证。 或者，Windows 帐户的模拟失败，因为在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户和 Windows 帐户的域之间没有完全信任关系。  
  
## <a name="user-action"></a>用户操作  
检查该 Windows 主体存在且没有拼写错误。  
  
如果此错误是由于在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户和 Windows 帐户的域之间缺乏完全信任关系所导致的，则执行以下操作之一可更正该错误：  
  
-   使用与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的 Windows 用户处于相同域中的帐户。  
  
-   如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在使用 Network Service 或 Local System 之类的计算机帐户，则包含 Windows 用户的域必须信任该计算机。  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帐户。  
  
