---
title: Integration Services (SSIS) 查询 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Query Builder [Integration Services]
- queries [Integration Services]
- statements [Integration Services]
- queries [Integration Services], about queries in packages
ms.assetid: 8822bd29-4575-46c8-92a0-1a39bc2604c1
caps.latest.revision: 57
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4188992529956ca06b22389dc4aadf1cc6ff6b7a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015479"
---
# <a name="integration-services-ssis-queries"></a>Integration Services (SSIS) 查询
  执行 SQL 任务、OLE DB 源、OLE DB 目标以及查找转换都可以使用 SQL 查询。 在执行 SQL 任务中，SQL 语句可以创建、更新和删除数据库对象与数据；运行存储过程以及执行 SELECT 语句。 在 OLE DB 源和查找转换中，SQL 语句通常为 SELECT 语句或 EXEC 语句。 后者经常用于运行可返回结果集的存储过程。  
  
 可以对查询进行分析，以确定它是否有效。 如果分析的查询使用到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的连接，则在分析、执行该查询后，执行结果（成功或失败）将分配给分析结果。 如果该查询使用的是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]之外的数据连接，则仅分析该语句。  
  
 SQL 语句可以通过直接在设计器中输入来定义，或通过指定文件连接或包含该语句的变量来定义。  
  
## <a name="direct-input-sql"></a>直接输入 SQL  
 查询生成器可用于执行 SQL 任务的用户界面中、OLE DB 源、OLE DB 目标和查找转换中。 查询生成器提供下列优势：  
  
-   以直观方式工作或使用 SQL 命令。  
  
     查询生成器包括多个图形窗格和一个文本窗格，前者用于直观地编写查询，后者用于显示查询的 SQL 文本。 您既可以在图形窗格中工作，也可以在文本窗格中工作。 查询生成器会同步这两个视图，因此查询文本和图形表示形式始终匹配。  
  
-   联接相关表。  
  
     如果将多个表添加到查询中，查询生成器将自动确定这些表之间的关系，并构造适当的联接命令。  
  
-   查询或更新数据库。  
  
     可以使用查询生成器利用 Transact-SQL SELECT 语句来返回数据，或使用查询生成器来创建可更新、添加或删除数据库记录的查询。  
  
-   即时查看和编辑结果。  
  
     可以执行查询，使用网格中可滚动浏览和编辑数据库中记录的记录集。  
  
 尽管表面上看查询生成器的作用仅限于创建 SELECT 查询，但您可以在文本窗格中键入其他类型的 SQL 语句，例如 DELETE 和 UPDATE。 图形窗格将自动更新，以反映您所键入的 SQL 语句。  
  
 通过在任务流或数据流组件对话框中或“属性”窗口中键入查询，您还可以提供直接输入。  
  
 有关详细信息，请参阅 [Query Builder](../../2014/integration-services/query-builder.md)。  
  
## <a name="sql-in-files"></a>文件形式的 SQL  
 执行 SQL 任务的 SQL 语句还可以驻留在单独的文件中。 例如，您可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中的查询编辑器等工具来编写查询，将查询保存到文件，然后在运行包时从该文件读取查询。 该文件可以只包含要运行的 SQL 语句以及注释。 若要使用存储在文件中的 SQL 语句，您必须提供指定文件名和位置的文件连接。 有关详细信息，请参阅 [File Connection Manager](connection-manager/file-connection-manager.md)。  
  
## <a name="sql-in-variables"></a>变量形式的 SQL  
 如果执行 SQL 任务中 SQL 语句的源是一个变量，您需要提供包含该查询的变量的名称。 该变量的 Value 属性包含查询文本。 可以将该变量的 ValueType 属性设置为字符串数据类型，然后键入 SQL 语句或将该语句复制到 Value 属性中。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](integration-services-ssis-variables.md)和[在包中使用变量](../../2014/integration-services/use-variables-in-packages.md)。  
  
  