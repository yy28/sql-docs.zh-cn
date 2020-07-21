---
title: MSSQLSERVER_17204 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17204 (Database Engine error)
ms.assetid: 40db66f9-dd5e-478c-891e-a06d363a2552
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a47d57dbd5e644a3594c00228a021ed937b5570d
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553597"
---
# <a name="mssqlserver_17204"></a>MSSQLSERVER_17204
    
## <a name="details"></a>详细信息  
  
|Attribute|值|  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|17204|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBLKIO_DEVOPENFAILED|  
|消息正文|%ls:无法打开文件号 %d 的文件 %ls。  操作系统错误: %ls。|  
  
## <a name="explanation"></a>说明  
 SQL Server 由于指定错误而无法打开指定的文件。  
  
## <a name="user-action"></a>用户操作  
 诊断并更正操作系统，然后重试该操作。  
  
  
