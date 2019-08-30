---
title: 使用数据库对象 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- database objects [SMO]
- objects [SMO]
ms.assetid: 702fd63d-8734-4a02-872e-aecfb037c787
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: db9333ec36ce9993ff0b8e3199ce5288a945d5e7
ms.sourcegitcommit: f3f83ef95399d1570851cd1360dc2f072736bef6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2019
ms.locfileid: "70148532"
---
# <a name="creating-altering-and-removing-database-objects"></a>创建、更改和删除数据库对象
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  创建 SMO 对象的各个阶段如下：  
  
1.  创建对象的实例。  
  
2.  设置对象属性。  
  
3.  创建子对象的实例。  
  
4.  设置子对象属性。  
  
5.  创建对象。  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 当在 smo 应用程序中创建 smo 对象的实例时, 它们在的实例[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]上不存在, 直到发出**Create**方法。 但是, 不需要为每个单独的对象发出**Create**方法。 如果对象具有一组子对象, 则只需父对象即可运行**Create**方法。 例如，表定义要求它至少包含一个列才能存在。 并且，列不能独立于表存在。 表与其列之间存在相互依赖的关系。  
  
 使用 <xref:Microsoft.SqlServer.Management.Dmf.Policy.Alter%2A> 方法可以更改对象。 对对象的若干更改（例如，向对象的集合之一添加子对象或更改属性值）将组成一批共同运行。 **Alter**方法减少了网络流量, 并提高了整体性能。  
  
 **Drop**语句用于删除最初创建该对象所需的对象及其所有相互依赖子对象。  
  
## <a name="see-also"></a>请参阅  
 [SMO 对象模型](../../../relational-databases/server-management-objects-smo/smo-object-model.md)  
  
  
