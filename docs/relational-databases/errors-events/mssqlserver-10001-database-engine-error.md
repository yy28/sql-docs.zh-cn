---
title: MSSQLSERVER_10001 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10001 (Database Engine error)
ms.assetid: f8fd2d8d-a4af-4b6a-ba51-9123b7e4c9bf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 30e93a4b5794aa8f14722f2e331331766b209590
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85781573"
---
# <a name="mssqlserver_10001"></a>MSSQLSERVER_10001
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|10001|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|HR_E_UNEXPECTED|  
|消息正文|提供程序报告了意外的灾难性错误。|  
  
## <a name="explanation"></a>说明  
分布式查询处理在调用 OLE DB 访问接口期间遇到一个一般性错误。  
  
## <a name="user-action"></a>用户操作  
使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 收集 OLE DB 跟踪事件并向 OLE DB 提供程序的产品支持人员提供此数据。  
  
## <a name="see-also"></a>另请参阅  
[SQL Server Profiler 模板和权限](~/tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)  
[SQL Server Native Client (OLE DB)](~/relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
