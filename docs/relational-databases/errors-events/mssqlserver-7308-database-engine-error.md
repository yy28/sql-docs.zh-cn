---
title: MSSQLSERVER_7308 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7308 (Database Engine error)
- single-threaded apartment mode
ms.assetid: cca9eab9-afb9-463d-abfd-0802257e2c99
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 64e662ebf9354f3d1ff48bb5870bd19d367dea9c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780213"
---
# <a name="mssqlserver_7308"></a>MSSQLSERVER_7308
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
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
  
