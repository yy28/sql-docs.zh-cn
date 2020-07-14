---
title: MSSQLSERVER_17132 | Microsoft Docs
description: SQL Server 计算机未能处理客户端登录数据包。 请查看错误的说明和可能的解决方法。
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17132 (Database Engine error)
ms.assetid: d1d198bd-6730-4394-bd5f-28f320c01a38
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4767ba217eab0d8cdbc6a9dc80f751868322f21f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780846"
---
# <a name="mssqlserver_17132"></a>MSSQLSERVER_17132
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|17132|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|INIT_NODESSPACE|  
|消息正文|由于没有足够的内存可用于描述符，导致服务器启动失败。 请减少不重要的内存负载或增加系统内存。|  
  
## <a name="explanation"></a>说明  
无法分配足够的内存来存储服务器内部描述符。  
  
## <a name="user-action"></a>用户操作  
在计算机中添加更多内存。 一般内存故障排除步骤可能会非常有用。  
  
