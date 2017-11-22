---
title: MSSQLSERVER_33027 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 33027 (Database Engine error)
ms.assetid: bfdc626e-7958-4511-987d-3b687824e8af
caps.latest.revision: "11"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6969b42ab8dedafba34b2ebaf52ceda628c3aa81
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver33027"></a>MSSQLSERVER_33027
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|33027|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SEC_CRYPTOPROV_CANTLOADDLL|  
|消息正文|由于 Authenticode 签名或文件路径无效，未能加载加密提供程序“%.*ls”。 请检查以前的消息，了解其他失败信息。|  
  
## <a name="explanation"></a>解释  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法使用错误消息中列出的加密提供程序，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法加载 DLL。 原因是名称无效或 Authenticode 签名无效。  
  
## <a name="user-action"></a>用户操作  
请检查该文件是否存在以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是否拥有访问该位置的权限。 请查看错误日志以获得其他相关消息。 否则，请联系加密服务供应商以获得详细信息。  
  
