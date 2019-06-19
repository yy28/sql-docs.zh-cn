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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7ecfcddc242bc9a30dd91acc7863e449ce82729
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62703996"
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
  
  
