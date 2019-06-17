---
title: 读取可重复的隔离级别的死锁 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- deadlocks in RDS [ADO]
- read repeatable in RDS [ADO]
ms.assetid: 29f3683f-12f3-4304-8a54-fe133c25a423
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 51899f0c3b37cf8228bb25ae8183d8f8e27ba4e0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699514"
---
# <a name="deadlocks-with-read-repeatable-isolation-level"></a>“读取可重复”隔离级别的死锁
如果自定义业务对象使用可重复读的隔离级别来访问 SQL Server，且业务对象的两个发送查询并在同一事务中更新的客户端同时调用，可能会出现死锁。 远程数据服务旨在允许一个进程超时以释放死锁，但该客户端的更新将失败。  
  
 使用[游标服务](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)**命令超时**要修改的超时长度，动态属性。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>请参阅  
 [RDS 基础知识](../../../ado/guide/remote-data-service/rds-fundamentals.md)



