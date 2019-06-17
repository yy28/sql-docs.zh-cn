---
title: 记录和流 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO]
- streams [ADO], about streams
- records [ADO]
ms.assetid: 4d68868e-2611-4b5c-9a89-7caa5f753151
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 19fc6e61a10e1a92f0f674a23d00f1e1b06a596c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701696"
---
# <a name="records-and-streams"></a>记录和流
当前提供的 ADO[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象作为访问数据源，如关系数据库中的信息的主要方式。 但是，某些访问接口支持[记录](../../../ado/reference/ado-api/record-object-ado.md)并[Stream](../../../ado/reference/ado-api/stream-object-ado.md)作为替代或补充对象可以与操作提供程序的数据的对象。 有关详细信息**记录**行为，请参阅提供程序的文档。  
  
## <a name="records"></a>记录  
 **记录**对象实质上是函数为一行**记录集**s。 但是，**记录**具有有限的功能相比**记录集**并且它们具有不同的属性和方法。中的数据源**记录**对象可以是从提供程序返回一个数据行的命令。 使用**记录**对象而非**记录集**对象返回一个数据行的查询从接收结果消除了实例化变得更加复杂的开销**记录集**对象。  
  
 **记录**对象可以用于尤其是对于传统的关系数据库以外的数据源的提供程序的其他用途，如[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 许多必须处理的信息，不作为表在数据库中，而是作为消息中存在电子邮件系统和文件流行文件系统中。 **记录**并**Stream**对象简化访问存储在关系数据库以外的源中的信息。  
  
 **记录**对象可以表示和管理文件系统或文件夹和消息中的电子邮件系统中的数据，例如目录和文件。 出于这些目的的源**记录**可以是一种开放的当前行**记录集**，绝对 URL 或打开与结合使用的相对 URL[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。  
  
 通常情况下，**记录集**可以用于表示容器或父文件夹或目录等的层次结构中。 一个**记录**可以用于在父容器，如文件或文档中返回一个节点有关的特定信息。 主要原因**记录**用于表示此类型的信息是异类数据的这些源。 这意味着，每个**记录**可能有不同的一组和字段数。 传统**记录集**包含行从数据库是同构的这意味着每一行都具有相同数量和类型的字段。  
  
 有关使用详细信息**记录**对象来处理此提供程序，如 Internet 发布提供程序中的异构数据，请参阅[用于 Internet 发布使用 ADO](../../../ado/guide/data/using-ado-for-internet-publishing.md)。  
  
## <a name="streams"></a>流  
 **Stream**对象提供了读取、 写入和管理的字节流的方法。 此字节流可以是文本或二进制文件，并仅受系统资源限制的大小。 通常情况下，ADO **Stream**对象用于以下目的：  
  
-   若要包含的数据**记录集**以 XML 格式保存。 从这些 XML 流保存**记录集**s 可以用作源，打开一个新时**记录集**。 有关详细信息，请参阅[流和暂留](../../../ado/guide/data/streams-and-persistence.md)。  
  
-   若要包含[CommandStreams](../../../ado/reference/ado-api/commandstream-property-ado.md)要作为一种替代方法在提供程序上执行[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)。 例如，XML Updategram 可以用作源对 Microsoft OLE DB 访问接口命令适用于 SQL Server。  
  
-   若要从一种格式中的提供程序而不接收结果**记录集**，例如 Microsoft OLE DB Provider for SQL Server 返回 XML 结果。 有关详细信息，请参阅[检索结果集流到](../../../ado/guide/data/retrieving-resultsets-into-streams.md)。  
  
-   若要包含的文本或包含的文件或消息，通常用于如 Microsoft OLE DB 访问接口的提供程序，用于 Internet 发布的字节数。 详细了解的这种用法**Stream**对象，请参阅[用于 Internet 发布使用 ADO](../../../ado/guide/data/using-ado-for-internet-publishing.md)。  
  
 一个**Stream**上可以打开对象：  
  
-   使用 URL 指定一个简单的文件。  
  
-   一个字段**记录**或**记录集**包含**Stream**对象。  
  
-   默认流**记录**或**记录集**对象，表示目录或复合文件。  
  
-   资源字段包含一个简单的文件的 URL。  
  
-   根本没有特定数据源。 在这种情况下， **Stream**在内存中打开对象。 可以向其中写入数据和则保存在另一个**Stream**或文件。  
  
-   中的 BLOB 字段**记录集**。  
  
 本部分包含以下主题。  
  
-   [流和暂留](../../../ado/guide/data/streams-and-persistence.md)  
  
-   [命令流](../../../ado/guide/data/command-streams.md)  
  
-   [检索流中的结果集](../../../ado/guide/data/retrieving-resultsets-into-streams.md)  
  
-   [使用 ADO 进行 Internet 发布](../../../ado/guide/data/using-ado-for-internet-publishing.md)
