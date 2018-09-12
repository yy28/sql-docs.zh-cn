---
title: XML 系统存储过程 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- system stored procedures [SQL Server], XML
- sp_xml_removedocument
- OPENXML statement, system stored procedures
- sp_xml_preparedocument
- XML [SQL Server], system stored procedures
ms.assetid: e60c7f85-6823-4d28-93d6-b053d08cc830
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d2e89e934fc8e1a476b7333ffe0c622465cabfe1
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43888873"
---
# <a name="xml-system-stored-procedures"></a>XML 系统存储过程
  SQL Server 提供了下列系统存储过程，可以与 OPENXML 一起使用：  
  
-   [sp_xml_preparedocument (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql)  
  
-   [sp_xml_removedocument (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql)  
  
 若要使用 OPENXML 编写查询，必须先通过调用 **sp_xml_preparedocument**来创建 XML 文档的内部表示形式。 该存储过程将返回 XML 文档的内部表示形式的句柄。 然后，将此句柄传递到 OPENXML。 OPENXML 将提供基于 XPath 的文档的行集视图。 具体而言，是一个行模式和一个或多个列模式。  
  
> [!NOTE]  
>  **sp_xml_preparedocument** 返回的文档句柄在会话的持续时间内有效。  
  
 通过调用 **sp_xml_removedocument** 系统存储过程可以从内存中删除 XML 文档的内部表示形式。  
  
## <a name="see-also"></a>请参阅  
 [OPENXML (Transact-SQL)](/sql/t-sql/functions/openxml-transact-sql)   
 [OPENXML (SQL Server)](../xml/openxml-sql-server.md)  
  
  
