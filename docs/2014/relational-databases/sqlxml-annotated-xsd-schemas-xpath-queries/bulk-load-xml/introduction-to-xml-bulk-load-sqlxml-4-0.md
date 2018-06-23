---
title: XML 大容量加载 (SQLXML 4.0) 简介 |Microsoft 文档
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- nontransacted XML Bulk Load operations
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
- transacted XML Bulk Load operations
- streaming XML data
ms.assetid: 38bd3cbd-65ef-4c23-9ef3-e70ecf6bb88a
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: cd67089959526afd3a983ba652d64e25be1403a6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123362"
---
# <a name="introduction-to-xml-bulk-load-sqlxml-40"></a>XML 大容量加载简介 (SQLXML 4.0)
  XML 大容量加载为独立的 COM 对象，您可以将半结构化的 XML 数据加载到 Microsoft[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]表。  
  
 您可以使用 INSERT 语句和 OPENXML 函数将 XML 数据插入到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库；但是，当需要插入大量 XML 数据时，大容量加载实用工具提供了更好的性能。  
  
 XML 大容量加载对象模型的 Execute 方法采用两个参数：  
  
-   带批注的 XML 架构定义 (XSD) 或 XML 数据精简 (XDR) 架构。 XML 大容量加载实用工具解释此映射架构和在标识要插入 XML 数据的 SQL Server 表时在该架构中指定的批注。  
  
-   XML 文档或文档片段（文档片段是没有单个顶级元素的文档）。 可以指定 XML 大容量加载可读取的文件名或流。  
  
 XML 大容量加载解释此映射架构，并标识要插入 XML 数据的表。  
  
 本部分假定您熟悉以下 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 功能：  
  
-   带批注的 XSD 架构和 XDR 架构。 有关带批注的 XSD 架构的详细信息，请参阅[简介带批注的 XSD 架构&#40;SQLXML 4.0&#41;](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)。 有关带批注的 XDR 架构的信息，请参阅[带批注的 XDR 架构&#40;SQLXML 4.0 中弃用&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 大容量插入机制，例如 [!INCLUDE[tsql](../../../includes/tsql-md.md)] BULK INSERT 语句和 bcp 实用工具。 有关详细信息，请参阅[大容量插入&#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/bulk-insert-transact-sql)和[bcp 实用工具](../../../tools/bcp-utility.md)。  
  
## <a name="streaming-of-xml-data"></a>对 XML 数据进行流式处理  
 由于源 XML 文档可能很大，因此无法将整个文档读入内存以进行大容量加载处理。 XML 大容量加载而是将 XML 数据解释为流并读取它。 当该实用工具读取数据时，该工具标识数据库表，并根据 XML 数据源生成相应记录，然后再将这些记录发送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以便插入。  
  
 例如，下面的源 XML 文档组成**\<客户 >** 元素和**\<顺序 >** 子元素：  
  
```  
<Customer ...>  
    <Order.../>  
    <Order .../>  
     ...  
</Customer>  
...  
```  
  
 当 XML 大容量加载读取**\<客户 >** 元素，它为 Customertable 生成一条记录。 当它读取 **\</Customer >** 结束标记，记录到表中的 XML 大容量加载插入[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 在相同方式，当它会读取**\<顺序 >** 元素，XML 大容量加载为 Ordertable，生成一条记录，然后插入到该记录[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]时读取表 **\</ 排序 >** 结束标记。  
  
## <a name="transacted-and-nontransacted-xml-bulk-load-operations"></a>事务和非事务 XML 大容量加载操作  
 XML 大容量加载可以以事务或非事务模式运行。 已在 nontransacted 模式下的大容量加载是否通常获得最佳性能： 即，事务属性设置为 FALSE)，并且以下条件之一为 true:  
  
-   要向其大容量加载数据的表为空，且没有任何索引。  
  
-   表具有数据和唯一索引。  
  
 非事务方法不能保证在大容量加载进程发生错误时回滚（但是可以进行部分回滚）。 非事务大容量加载适用于数据库为空的情况。 因此，如果发生错误，您可以清除数据库并重新启动 XML 大容量加载。  
  
> [!NOTE]  
>  在非事务模式下，XML 大容量加载使用并提交默认的内部事务。 当事务属性设置为 TRUE 时，XML 大容量加载不调用此事务的提交。  
  
 如果事务属性设置为 TRUE，则 XML 大容量加载创建临时文件，一个用于标识映射架构中每个表。 XML 大容量加载首先将源 XML 文档中的记录存储到这些临时文件中。 接着，[!INCLUDE[tsql](../../../includes/tsql-md.md)] BULK INSERT 语句检索这些文件中的上述记录，并将其存储到相应的表中。 可以通过使用 TempFilePath 属性来指定这些临时文件的位置。 您必须确保用于 XML 大容量加载的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 帐户有权访问此路径。 如果未指定 TempFilePath 属性，TEMP 环境变量中指定的默认文件路径用于创建临时文件。  
  
 如果事务属性设置为 FALSE （默认设置），将 XML 大容量加载使用大容量加载数据的 OLE DB 接口 IRowsetFastLoad。  
  
 如果 ConnectionString 属性设置为连接字符串，并且事务属性设置为 TRUE，XML 大容量加载操作在其自己的事务上下文中。 （例如，XML 大容量加载启动其自己的事务，并根据需要提交或回滚。）  
  
 如果 ConnectionCommand 属性设置与现有的连接对象和事务属性的连接设置为 TRUE，XML 大容量加载不会分别颁发对于成功或失败，提交或回滚语句。 如果出现错误，XML 大容量加载则返回相应的错误消息。 执行 COMMIT 或 ROLLBACK 语句由启动该大容量加载的客户端决定。 用于 XML 大容量加载的连接对象应是类型 ICommand 的或者是 ADO 命令对象。  
  
 在 SQLXML 4.0 中，ConnectionObject 不能与使用事务属性设置为 FALSE。 因为无法对传入的会话打开多个 IRowsetFastLoad 接口与 ConnectionObject nontransacted 模式不支持。  
  
  
