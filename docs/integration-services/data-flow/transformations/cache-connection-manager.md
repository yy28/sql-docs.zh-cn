---
title: "缓存连接管理器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "缓存连接管理器"
ms.assetid: bdc92038-3720-4795-8a5c-79b963f2c952
caps.latest.revision: 23
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 23
---
# 缓存连接管理器
  缓存连接管理器从缓存转换或从缓存文件 (.caw) 中读取数据，并可将数据保存到缓存文件。 无论是否将缓存连接管理器配置为使用缓存文件，数据都会始终存储在内存中。  
  
 “缓存转换”转换可以将数据流中已连接数据源的数据写入缓存连接管理器。 包中的查找转换会对数据执行查找。  
  
> [!NOTE]  
>  缓存连接管理器不支持二进制大型对象 (BLOB) 数据类型 DT_TEXT、DT_NTEXT 和 DT_IMAGE。 如果引用数据集包含 BLOB 数据类型，则运行包时该组件将失败。 可以使用 **“缓存连接管理器编辑器”** 修改列数据类型。 有关详细信息，请参阅 [Cache Connection Manager Editor](../../../integration-services/data-flow/transformations/cache-connection-manager-editor.md)。  
  
> [!NOTE]  
>  包的保护级别不适用于缓存文件。 如果缓存文件包含敏感信息，可使用访问控制列表 (ACL) 来限制对存储该文件的位置或文件夹的访问。 应只允许访问某些帐户。 有关详细信息，请参阅[访问包使用的文件](../../../integration-services/security/access-to-files-used-by-packages.md)。  
  
## 缓存连接管理器的配置  
 可以用下列方式配置缓存连接管理器：  
  
-   指示是否使用缓存文件。  
  
     如果将缓存连接管理器配置为使用缓存文件，则连接管理器将执行下列操作之一：  
  
    -   若将“缓存转换”转换配置为将数据从数据流中的某个数据源写入缓存连接管理器，则将数据保存到该文件。  
  
    -   从缓存文件读取数据。  
  
     有关详细信息，请参阅 [Cache Transform](../../../integration-services/data-flow/transformations/cache-transform.md)。  
  
-   更改缓存中存储的列的元数据。  
  
-   使用表达式在运行时更新缓存文件名，以设置 ConnectionString 属性。 有关详细信息，请参阅[在包中使用属性表达式](../../../integration-services/expressions/use-property-expressions-in-packages.md)。  
  
 可以通过 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 设计器中设置的属性的详细信息，请参阅[缓存连接管理器编辑器](../../../integration-services/data-flow/transformations/cache-connection-manager-editor.md)。  
  
 有关如何以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和[以编程方式添加连接](../../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
## 相关任务  
 [在完全缓存模式下使用缓存连接管理器实现查找转换](../../../integration-services/data-flow/transformations/lookup transformation full cache mode - cache connection manager.md)  
  
  