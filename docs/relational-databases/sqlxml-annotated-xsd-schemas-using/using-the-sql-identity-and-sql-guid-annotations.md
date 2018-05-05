---
title: 使用 sql:identity 和 sql:guid 批注 |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sql:guid
- annotated XSD schemas, IDENTITY-type columns
- annotated XSD schemas, GUID values
- DiffGrams [SQLXML], annotations
- identity annotation
- XSD schemas [SQLXML], GUID values
- GUIDs [SQLXML]
- guid annotation
- sql:identity
- IDENTITY-type column
- XSD schemas [SQLXML], IDENTITY-type columns
- updategrams [SQLXML], GUID values
ms.assetid: 7661dfd0-6573-4692-a8f1-3597adcd33c4
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: da967220c77451d807a79d2e10701fd1f76791d2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>使用 sql:identity 和 sql:guid 批注
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  你可以指定**sql:identity**和**sql:guid**中 XSD 架构映射到数据库列中的任何节点上的批注[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 而属的 updategram 格式支持**updg： 在标识**和**updg:guid**特性，DiffGram 格式却没有。 **Updg： 在标识**属性更新标识类型列中定义的行为。 **Updg:guid**属性允许你获取 GUID 值从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和在属的 updategram 中使用它。 有关详细信息和工作示例，请参阅[插入数据使用 XML Updategram &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)。  
  
 **Sql:identity**和**sql:guid**批注将此功能扩展到 Diffgram。  
  
 执行 DiffGram 时，应首先将其转换为 updategram，然后再执行该 updategram。 通过指定**sql:identity**和**sql:guid** XSD 架构中的批注，您处于事实定义属的 updategram 的行为。 因此，所有批注都在 updategram 的上下文中进行描述。 这些批注可用于 DiffGram 和 updategram；但是，updategram 已提供了一种更强大的处理标识和 GUID 值的方式。  
  
 **Sql:identity**和**sql:guid**批注可以定义复杂内容元素上。  
  
## <a name="sqlidentity-annotation"></a>sql:identity 批注  
 你可以指定**sql:identity**中映射到的标识类型数据库列的任何节点上的 XSD 架构的批注。 为该批注指定的值定义如何更新 IDENTITY 类型的列（通过使用 updategram 中提供的值来修改列，或者通过忽略该值而针对该列采用由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生成的值）。  
  
 **Sql:identity**批注可以分配两个值：  
  
 ignore  
 指示 updategram 忽略在其中为该列提供的任何值，并依赖于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生成标识值。  
  
 useValue  
 指示 updategram 使用在其中提供的值来更新 IDENTITY 类型的列。 updategram 不会检查列是否为标识值。  
  
 如果属的 updategram 指定标识类型列中，值**sql:identity ="useValue"** 必须架构中指定。  
  
## <a name="sqlguid-annotation"></a>sql:guid 批注  
 updategram 可以使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生成一个 GUID 值，并将此值用于该 updategram 中。 在 Diffgram 的上下文，你可以使用**sql:guid**批注以指定是否使用由 SQL Server 生成的 GUID 值，或使用将该列的情况下属的 updategram 中提供的值。  
  
 **Sql:guid**批注可以分配两个值：  
  
 generate  
 指定应在更新操作中使用由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生成的该列的 GUID。  
  
 useValue  
 指定在 updategram 中指定的值可以用于该列。 这是默认值。  
  
  
