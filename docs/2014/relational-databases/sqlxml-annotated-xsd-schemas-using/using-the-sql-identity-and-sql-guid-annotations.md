---
title: '使用 sql: identity 和 sql: guid 批注 |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bb953042707054a7dbfdee697b986e7e65f7059b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62718004"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>使用 sql:identity 和 sql:guid 批注
  您可以指定`sql:identity`并`sql:guid`映射到数据库列中的任何节点上的 XSD 架构中的批注[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 updategram 格式支持 `updg:at-identity` 和 `updg:guid` 属性，而 DiffGram 格式不支持这些属性。 `updg:at-identity` 属性定义在更新 IDENTITY 类型列时的行为。 `updg:guid` 属性使您可以获取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 GUID 值，并将其用于 updategram 中。 有关详细信息和工作示例，请参阅[使用 XML Updategram 插入数据&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)。  
  
 `sql:identity` 和 `sql:guid` 批注将此功能扩展至 DiffGram。  
  
 执行 DiffGram 时，应首先将其转换为 updategram，然后再执行该 updategram。 通过在 XSD 架构中指定 `sql:identity` 和 `sql:guid` 批注，您实际上正在定义 updategram 的行为。 因此，所有批注都在 updategram 的上下文中进行描述。 这些批注可用于 DiffGram 和 updategram；但是，updategram 已提供了一种更强大的处理标识和 GUID 值的方式。  
  
 可以针对复杂内容元素定义 `sql:identity` 和 `sql:guid` 批注。  
  
## <a name="sqlidentity-annotation"></a>sql:identity 批注  
 您可以在映射到 IDENTITY 类型的数据库列的任何节点上的 XSD 架构中指定 `sql:identity` 批注。 为此批注指定的值定义如何更新 IDENTITY 类型的列 (通过使用在 updategram 中提供的值来修改列或通过在这种情况下忽略该值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-生成的值用于此列)。  
  
 可以为 `sql:identity` 批注分配两个值：  
  
 ignore  
 指示 updategram 忽略在其中为该列提供的任何值，并依赖于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生成标识值。  
  
 useValue  
 指示 updategram 使用在其中提供的值来更新 IDENTITY 类型的列。 updategram 不会检查列是否为标识值。  
  
 如果 updategram 已为 IDENTITY 类型的列指定值，必须在该架构中指定 `sql:identity="useValue"`。  
  
## <a name="sqlguid-annotation"></a>sql:guid 批注  
 updategram 可以使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生成一个 GUID 值，并将此值用于该 updategram 中。 在 DiffGram 上下文中，您可以使用 `sql:guid` 批注指定是使用由 SQL Server 生成的 GUID 值还是使用在 updategram 中为该列提供的值。  
  
 可以为 `sql:guid` 批注分配两个值：  
  
 generate  
 指定应在更新操作中使用由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 生成的该列的 GUID。  
  
 useValue  
 指定在 updategram 中指定的值可以用于该列。 这是默认值。  
  
  
