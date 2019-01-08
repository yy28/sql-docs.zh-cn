---
title: 使用数据库对象 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- database objects [SMO]
- objects [SMO]
ms.assetid: 702fd63d-8734-4a02-872e-aecfb037c787
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5bf11ece3797f9bbc580339846efb685876b2d0f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52788219"
---
# <a name="working-with-database-objects"></a>使用数据库对象
  创建 SMO 对象的各个阶段如下：  
  
1.  创建对象的实例。  
  
2.  设置对象属性。  
  
3.  创建子对象的实例。  
  
4.  设置子对象属性。  
  
5.  创建对象。  
  
 当在 SMO 应用程序中创建 SMO 对象的实例时，在发出 `Create` 方法之前，这些实例不会存在于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例中。 但是，不必针对每个单独的对象发出 `Create` 方法。 如果某一对象具有一组子对象，则只需要父对象运行 `Create` 方法。 例如，表定义要求它至少包含一个列才能存在。 并且，列不能独立于表存在。 表与其列之间存在相互依赖的关系。  
  
 使用 <xref:Microsoft.SqlServer.Management.Dmf.Policy.Alter%2A> 方法可以更改对象。 对对象的若干更改（例如，向对象的集合之一添加子对象或更改属性值）将组成一批共同运行。 `Alter` 方法减少了网络流量，并提高了整体性能。  
  
 `Drop` 语句用于删除最初创建该对象所需的对象及其相互依赖的所有子对象。  
  
## <a name="see-also"></a>请参阅  
 [SMO 对象模型](../smo-object-model.md)  
  
  
