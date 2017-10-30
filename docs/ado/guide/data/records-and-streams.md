---
title: "记录和流 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- streams [ADO]
- streams [ADO], about streams
- records [ADO]
ms.assetid: 4d68868e-2611-4b5c-9a89-7caa5f753151
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d11617fc364b3ce9f2c4f5b37623f4c74f968517
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="records-and-streams"></a>记录和流
当前提供的 ADO[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象作为访问数据源，例如关系数据库中的信息的主要方式。 但是，某些提供程序支持[记录](../../../ado/reference/ado-api/record-object-ado.md)和[流](../../../ado/reference/ado-api/stream-object-ado.md)作为可与其操作提供程序的数据的替代或补充对象的对象。 有关详细信息上**记录**行为，请参阅提供程序的文档。  
  
## <a name="records"></a>记录  
 **记录**对象实质上是函数为一行**记录集**s。 但是，**记录**具有有限的功能相比**记录集**并且它们具有不同的属性和方法。中的数据的源**记录**对象可以是从提供程序返回的数据的一个行的命令。 使用**记录**对象而非**记录集**要接收来自返回一行数据的查询的结果对象消除了实例化变得更加复杂的开销**记录集**对象。  
  
 **记录**对象可以用于特别是对于传统的关系数据库除外的数据源的提供程序的其他用途，如[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 很多必须处理的信息，不作为表在数据库中，而是作为消息中存在电子邮件系统和文件现代文件系统中。 **记录**和**流**对象便于访问存储在关系数据库以外的源的信息。  
  
 **记录**对象可以表示和管理文件系统或文件夹和消息的电子邮件系统中的数据，例如目录和文件。 出于这些目的的源**记录**可以是已打开的当前行**记录集**，绝对 URL 或相对 URL 结合打开[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。  
  
 通常情况下，**记录集**可以用于表示容器或如文件夹或目录层次结构中的父级。 A**记录**可以用于在父容器，如文件或文档中返回一个节点有关的特定信息。 主要原因**记录**用于表示此类型的信息是这些源的数据是异类。 这意味着，每个**记录**可能有不同的一组和字段的数目。 传统**记录集**包含行从数据库是同构的这意味着每个行具有相同数量和类型的字段。  
  
 有关使用**记录**对象处理从提供程序如 Internet 发布提供此异类数据，请参阅[用于 Internet 发布使用 ADO](../../../ado/guide/data/using-ado-for-internet-publishing.md)。  
  
## <a name="streams"></a>流  
 **流**对象提供读取、 写入和管理的字节流的方式。 此字节流可能是文本或二进制文件，并且的大小仅受系统资源限制。 通常情况下，ADO**流**对象用于下列目的：  
  
-   若要包含的数据**记录集**以 XML 格式保存。 从这些 XML 流保存**记录集**s 可以用作源，打开一个新时**记录集**。 有关详细信息，请参阅[流和持久性](../../../ado/guide/data/streams-and-persistence.md)。  
  
-   若要包含[CommandStreams](../../../ado/reference/ado-api/commandstream-property-ado.md)作为一种替代方法在提供程序上执行[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)。 例如，XML Updategram 可作为源用于对 Microsoft OLE DB 访问接口的命令为 SQL Server。  
  
-   若要从一种格式中的提供程序中以外接收结果**记录集**，如从 Microsoft OLE DB Provider for SQL Server 的 XML 结果。 有关详细信息，请参阅[分成流检索结果集](../../../ado/guide/data/retrieving-resultsets-into-streams.md)。  
  
-   若要包含的文本或构成一个文件或消息，通常用于如 Microsoft OLE DB 访问接口的提供程序，为 Internet 发布的字节。 有关详细信息有关的这种用法**流**对象，请参阅[用于 Internet 发布使用 ADO](../../../ado/guide/data/using-ado-for-internet-publishing.md)。  
  
 A**流**对象可以打开上：  
  
-   使用 URL 指定一个简单的文件。  
  
-   字段**记录**或**记录集**包含**流**对象。  
  
-   默认流**记录**或**记录集**表示目录或复合文件的对象。  
  
-   包含一个简单的文件的 URL 的资源字段。  
  
-   根本没有特定数据源。 在这种情况下，**流**在内存中打开对象。 可以向其中写入数据的位置，然后保存在另一个**流**或文件。  
  
-   中的 BLOB 字段**记录集**。  
  
 本部分包含以下主题。  
  
-   [流和持久性](../../../ado/guide/data/streams-and-persistence.md)  
  
-   [命令流](../../../ado/guide/data/command-streams.md)  
  
-   [到流中检索结果集](../../../ado/guide/data/retrieving-resultsets-into-streams.md)  
  
-   [ADO 用于 Internet 发布](../../../ado/guide/data/using-ado-for-internet-publishing.md)

