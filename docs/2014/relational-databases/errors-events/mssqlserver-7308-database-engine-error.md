---
title: MSSQLSERVER_7308 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 7308 (Database Engine error)
- single-threaded apartment mode
ms.assetid: cca9eab9-afb9-463d-abfd-0802257e2c99
caps.latest.revision: 7
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6a85c217cc88367f287b2d60ee56be4183ea1850
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017952"
---
# <a name="mssqlserver7308"></a>MSSQLSERVER_7308
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|7308|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|RMT_STA_DISABLED|  
|消息正文|因为 OLE DB 访问接口“%ls”配置为在单线程单元模式下运行，所以该访问接口无法用于分布式查询。|  
  
## <a name="explanation"></a>解释  
 您使用了配置为在单线程单元 (STA) 模式下运行的 OLE DB 访问接口。 在单线程单元 (STA) 模式下运行的 OLE DB 访问接口无法用于分布式查询。  
  
## <a name="user-action"></a>用户操作  
 若要解决此错误，请将该访问接口配置为在多线程单元 (MTA) 模式下运行。 如果该提供程序不支持 MTA，且无法升级到支持 MTA 的版本，请考虑将该提供程序配置为在进程外运行。 该提供程序的供应商应能够告知你该提供程序是支持 MTA 还是在进程外运行。  
  
  