---
title: 数据收集器编程 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data collector [SQL Server], programming
ms.assetid: 53b4752b-055d-4716-b2bc-75b4cce84101
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a9a3e4428eee6057ac3e38e553eec43616504a06
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129725"
---
# <a name="data-collector-programming"></a>数据收集器编程
  <xref:Microsoft.SqlServer.Management.Collector> 中的数据收集器 API 允许通过对象模型来对所有配置操作进行编程控制。 此外，很多使用此 API 的数据收集操作都是以服务器上安装的存储过程方式实现的。  
  
 下图显示数据收集器对象模型的关键元素：  
  
 ![数据收集器对象模型](../../../2014/database-engine/dev-guide/media/dc-objectmodel.gif "数据收集器对象模型")  
  
  