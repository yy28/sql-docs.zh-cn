---
title: MSSQLSERVER_33027 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 33027 (Database Engine error)
ms.assetid: bfdc626e-7958-4511-987d-3b687824e8af
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f6bb461b42b66368224fffd2c14f9b4da61abf5b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85033861"
---
# <a name="mssqlserver_33027"></a>MSSQLSERVER_33027
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|33027|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SEC_CRYPTOPROV_CANTLOADDLL|  
|消息正文|由于 Authenticode 签名或文件路径无效，未能加载加密提供程序“%.*ls”。 请检查以前的消息，了解其他失败信息。|  
  
## <a name="explanation"></a>说明  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法使用错误消息中列出的加密提供程序，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法加载 DLL。 原因是名称无效或 Authenticode 签名无效。  
  
## <a name="user-action"></a>用户操作  
 请检查该文件是否存在以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是否拥有访问该位置的权限。 请查看错误日志以获得其他相关消息。 否则，请联系加密服务供应商以获得详细信息。  
  
  
