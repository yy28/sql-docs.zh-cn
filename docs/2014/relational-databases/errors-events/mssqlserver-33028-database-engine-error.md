---
title: MSSQLSERVER_33028 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 33028 (Database Engine error)
ms.assetid: c5cec0e4-0bcd-4907-826f-e7d835cfcb37
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b2820abe304ce16234029caa16164285f6f66f9b
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37415317"
---
# <a name="mssqlserver33028"></a>MSSQLSERVER_33028
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|33028|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SEC_CRYPTOPROV_CANTOPENSESSION|  
|消息正文|无法为 %S_MSG '%.*ls' 打开会话。 提供程序错误代码: %d。|  
  
## <a name="explanation"></a>解释  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法打开错误消息中列出的加密提供程序。 加密提供程序提供的错误代码如下所示。 您可能需要联系您的加密服务供应商以获得有关错误的详细信息。  
  
|错误代码|Description|  
|----------------|-----------------|  
|0|成功。 没有错误。|  
|@shouldalert|失败。 出现了未指定的错误或意外错误。 无法获得其他信息。|  
|2|缓冲区不足。 无法为加密提供程序分配空间。|  
|3|不提供支持。 此版本不支持该加密提供程序。 请选择其他加密提供程序。|  
|4|找不到该加密提供程序。 指定的加密提供程序不存在或您无权访问这些文件。|  
|5|授权失败。 可能是创建凭据时提供了不正确的密码或用户名所致。 也可能是凭据不存在所致。|  
|6|参数无效。 传递到加密提供程序的参数无效。|  
  
## <a name="user-action"></a>用户操作  
 解决该错误，或联系加密服务提供商以获得详细信息。  
  
  
