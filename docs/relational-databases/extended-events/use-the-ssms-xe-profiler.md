---
title: 使用 SSMS XEvent 探查器 | Microsoft Docs
ms.custom: ''
ms.date: 10/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: genemi
ms.suite: sql
ms.technology: xevents
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], system health session
- extended events [SQL Server], system_health session
- system_health session [SQL Server extended events]
- system health session [SQL Server extended events]
ms.assetid: 1e1fad43-d747-4775-ac0d-c50648e56d78
author: yualan
ms.author: alayu
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 46395f2d8125a8c92487f3995808d12a42c7298c
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43078239"
---
# <a name="use-the-ssms-xevent-profiler"></a>使用 SSMS XEvent 探查器
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
XEvent 探查器是 SQL Server Management Studio (SSMS) 的功能，可显示扩展事件的实时查看器窗口。 本概述描述了使用此探查器的原因、关键功能以及查看扩展事件的入门说明。

## <a name="why-would-i-use-the-xevent-profiler"></a>使用 XEvent 探查器的原因
不同于 SQL 探查器，XEvent 探查器直接集成到 SSMS，基于 SQL 引擎中可缩放的扩展事件技术。 此功能可以快速访问 SQL 服务器上诊断事件的实时传送视频流视图。 此视图可自定义，并且自定义项可以 .viewsettings 文件的形式与其他 SSMS 用户共享。 使用 XE 探查器创建的会话与使用 SQL 探查器时类似的 SQL 跟踪相比，对运行的 SQL 服务器具有更低的侵入性。 用户也可以使用现有的 XE 会话属性 UI 或通过 TSQL 自定义此会话。

## <a name="prerequisites"></a>必备条件
此功能仅在 SQL Server Management Studio (SSMS) v17.3 或更高版本中可用。 请确保使用最新版本。 可以在[此处](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)找到最新版本。

## <a id="getting-started"></a>入门
若要访问 XEvent 探查器，请执行以下步骤：

1. 打开 SQL Server Management Studio。

2. 连接 SQL Server 数据库引擎实例或 localhost。

3. 在对象资源管理器中，找到 XE 探查器菜单项，点击“+”号将其展开。

   ![XEProfiler 菜单](media/xevents-xe-profiler-menu.png)

4. 若想要在会话中查看所有扩展事件，双击“标准”。 若想要查看记录的 SQL 语句，单击“T-SQL”。 如果尚未创建会话，将为你创建一个。

   ![XEProfiler 会话](media/xevents-xe-profiler-start-session.png)

5. 现在可以查看扩展事件。

   ![XEProfiler 查看器](media/xevents-xe-profiler-start-viewer.png)

## <a name="see-also"></a>另请参阅
[扩展事件](../../relational-databases/extended-events/extended-events.md)  
[扩展事件工具](../../relational-databases/extended-events/extended-events-tools.md)  
  
  
