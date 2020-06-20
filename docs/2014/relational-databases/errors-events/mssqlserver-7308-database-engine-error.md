---
title: MSSQLSERVER_7308 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7308 (Database Engine error)
- single-threaded apartment mode
ms.assetid: cca9eab9-afb9-463d-abfd-0802257e2c99
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9978f35ebe41eeda1470220772f87e83ab1ad942
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053768"
---
# <a name="mssqlserver_7308"></a>MSSQLSERVER_7308
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|7308|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|RMT_STA_DISABLED|  
|消息正文|因为 OLE DB 访问接口“%ls”配置为在单线程单元模式下运行，所以该访问接口无法用于分布式查询。|  
  
## <a name="explanation"></a>说明  
 您使用了配置为在单线程单元 (STA) 模式下运行的 OLE DB 访问接口。 在单线程单元 (STA) 模式下运行的 OLE DB 访问接口无法用于分布式查询。  
  
## <a name="user-action"></a>用户操作  
 若要解决此错误，请将该访问接口配置为在多线程单元 (MTA) 模式下运行。 如果该提供程序不支持 MTA，且无法升级到支持 MTA 的版本，请考虑将该提供程序配置为在进程外运行。 该提供程序的供应商应能够告知你该提供程序是支持 MTA 还是在进程外运行。  
  
  
