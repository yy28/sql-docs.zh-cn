---
title: XML 系统存储过程 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- system stored procedures [SQL Server], XML
- sp_xml_removedocument
- OPENXML statement, system stored procedures
- sp_xml_preparedocument
- XML [SQL Server], system stored procedures
ms.assetid: e60c7f85-6823-4d28-93d6-b053d08cc830
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: de9c0bb15963ecfa170c6079a95bfc446cb14f3b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47787765"
---
# <a name="xml-system-stored-procedures"></a>XML 系统存储过程
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  SQL Server 提供了下列系统存储过程，可以与 OPENXML 一起使用：  
  
-   [sp_xml_preparedocument (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)  
  
-   [sp_xml_removedocument (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql.md)  
  
 若要使用 OPENXML 编写查询，必须先通过调用 **sp_xml_preparedocument**来创建 XML 文档的内部表示形式。 该存储过程将返回 XML 文档的内部表示形式的句柄。 然后，将此句柄传递到 OPENXML。 OPENXML 将提供基于 XPath 的文档的行集视图。 具体而言，是一个行模式和一个或多个列模式。  
  
> [!NOTE]  
>  **sp_xml_preparedocument** 返回的文档句柄在会话的持续时间内有效。  
  
 通过调用 **sp_xml_removedocument** 系统存储过程可以从内存中删除 XML 文档的内部表示形式。  
  
## <a name="see-also"></a>另请参阅  
 [OPENXML (Transact-SQL)](../../t-sql/functions/openxml-transact-sql.md)   
 [OPENXML (SQL Server)](../../relational-databases/xml/openxml-sql-server.md)  
  
  
