---
title: 缓存连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Cache connection manager
ms.assetid: bdc92038-3720-4795-8a5c-79b963f2c952
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1026f4c20042a9aec24256238190dd1a230bda42
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62833587"
---
# <a name="cache-connection-manager"></a>缓存连接管理器
  缓存连接管理器从缓存转换或从缓存文件 (.caw) 中读取数据，并可将数据保存到缓存文件。 无论是否将缓存连接管理器配置为使用缓存文件，数据都会始终存储在内存中。  
  
 “缓存转换”转换可以将数据流中已连接数据源的数据写入缓存连接管理器。 包中的查找转换会对数据执行查找。  
  
> [!NOTE]  
>  缓存连接管理器不支持二进制大型对象 (BLOB) 数据类型 DT_TEXT、DT_NTEXT 和 DT_IMAGE。 如果引用数据集包含 BLOB 数据类型，则运行包时该组件将失败。 可以使用 **“缓存连接管理器编辑器”** 修改列数据类型。 有关详细信息，请参阅 [Cache Connection Manager Editor](../cache-connection-manager-editor.md)。  
  
> [!NOTE]  
>  包的保护级别不适用于缓存文件。 如果缓存文件包含敏感信息，可使用访问控制列表 (ACL) 来限制对存储该文件的位置或文件夹的访问。 应只允许访问某些帐户。 有关详细信息，请参阅 [访问包使用的文件](../access-to-files-used-by-packages.md)。  
  
## <a name="configuration-of-the-cache-connection-manager"></a>缓存连接管理器的配置  
 可以用下列方式配置缓存连接管理器：  
  
-   指示是否使用缓存文件。  
  
     如果将缓存连接管理器配置为使用缓存文件，则连接管理器将执行下列操作之一：  
  
    -   若将“缓存转换”转换配置为将数据从数据流中的某个数据源写入缓存连接管理器，则将数据保存到该文件。  
  
    -   从缓存文件读取数据。  
  
     有关详细信息，请参阅 [Cache Transform](../data-flow/transformations/cache-transform.md)。  
  
-   更改缓存中存储的列的元数据。  
  
-   使用表达式在运行时更新缓存文件名，以设置 ConnectionString 属性。 有关详细信息，请参阅 [在包中使用属性表达式](../expressions/use-property-expressions-in-packages.md)。  
  
 可以通过 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 设计器中设置的属性的详细信息，请参阅 [缓存连接管理器编辑器](../cache-connection-manager-editor.md)。  
  
 有关如何以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和[以编程方式添加连接](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
 [在完全缓存模式下使用缓存连接管理器实现查找转换](lookup-transformation-full-cache-mode-ole-db-connection-manager.md)  
  
  
