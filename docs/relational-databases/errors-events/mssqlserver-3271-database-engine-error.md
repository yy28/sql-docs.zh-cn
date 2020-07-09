---
title: MSSQLSERVER_3271 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3271 (Database Engine error)
ms.assetid: 21b8de4b-6624-4163-9561-1a6cc8fe3d51
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: dd557a391b82ceb5575ad13c6d065583105df52a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723628"
---
# <a name="mssqlserver_3271"></a>MSSQLSERVER_3271
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|3271|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DMPIO_IO_ERROR|  
|消息正文|在文件 "%ls:" 上发生不可恢复的 I/O 错误: %ls。|  
  
## <a name="explanation"></a>说明  
这是一个一般错误，是在操作系统在备份或还原操作过程中执行 I/O 的同时引发错误时出现的。 在大多数情况下，原因仅仅是备份介质已满。  
  
该错误可能包含来自操作系统的其他文本，指示磁盘已满。 在使用第三方备份软件执行备份或还原操作时，可能会出现指示备份失败的其他消息。 该消息可能与以下文本类似：  
  
```  
"2005-08-02 16:05:16.04 spid55 Error: 18210, Severity: 16, State: 1.  
 2005-08-02 16:05:16.04 spid55 BackupVirtualDeviceFile  
::RequestDurableMedia: Flush failure on backup device 'VDINULL'.   
Operating system error 995(The I/O operation has been aborted because   
of either a thread exit or an application request.)."  
```  
  
这指示备份软件要求终止备份或还原操作。  
  
## <a name="user-action"></a>用户操作  
根据需要执行以下任务：  
  
-   检查基础系统错误消息和在此错误前面的 SQL Server 错误消息以查明失败的原因。  
  
-   确保备份和还原介质具有足够的空间。  
  
-   更正由第三方备份和还原软件引发的任何错误。  
  
