---
title: "使用数据库对象 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- database objects [SMO]
- objects [SMO]
ms.assetid: 702fd63d-8734-4a02-872e-aecfb037c787
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d9b2565474a777bbaddc6b659227a88bc1d2d609
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="creating-altering-and-removing-database-objects"></a>创建、 更改和删除数据库对象
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]SMO 对象创建的阶段如下所示：  
  
1.  创建对象的实例。  
  
2.  设置对象属性。  
  
3.  创建子对象的实例。  
  
4.  设置子对象属性。  
  
5.  创建对象。  
  
 当 SMO 应用程序中创建的 SMO 对象实例时，它们不存在的实例上[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]直到**创建**颁发方法。 但是，不需要发出**创建**为每个单独的对象的方法。 如果对象具有一组子对象，则必须仅父对象以运行**创建**方法。 例如，表定义要求它至少包含一个列才能存在。 并且，列不能独立于表存在。 表与其列之间存在相互依赖的关系。  
  
 使用 <xref:Microsoft.SqlServer.Management.Dmf.Policy.Alter%2A> 方法可以更改对象。 对对象的若干更改（例如，向对象的集合之一添加子对象或更改属性值）将组成一批共同运行。 **Alter**方法可减少网络流量并提高总体性能。  
  
 **删除**语句用于移除一个对象和所需最初创建对象所有 codependent 子对象。  
  
## <a name="see-also"></a>另请参阅  
 [SMO 对象模型](../../../relational-databases/server-management-objects-smo/smo-object-model.md)  
  
  
