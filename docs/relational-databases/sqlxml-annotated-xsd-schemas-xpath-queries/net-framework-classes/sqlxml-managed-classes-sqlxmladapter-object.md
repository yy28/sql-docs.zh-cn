---
title: SqlXmlAdapter 对象 （SQLXML 托管类） |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- void Update(DataSet ds) method
- SqlXmlAdapter object
- void Fill(DataSet ds) method
- SQLXML Managed Classes, SqlXmlAdapter object
- Managed Classes [SQLXML], SqlXmlAdapter object
ms.assetid: 0a16eddf-fc26-4d92-82d4-359b5fb905d5
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3240c1e0d553bb0bdcc97d529dfee92d89332908
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlxml-managed-classes---sqlxmladapter-object"></a>SQLXML 托管类-SqlXmlAdapter 对象
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  此对象提供用于促进与 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 中的数据集进行交互的方法。 有关工作示例，请参阅[.NET 环境中访问 SQLXML 功能](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md)。  
  
 SqlXmlAdapter 对象支持这些方法：  
  
 void 填充 (数据集 ds)  
 用从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 检索的 XML 数据填充 .NET Framework 中的数据集。  
  
 void 更新 (数据集 ds)  
 用数据集中的数据更新 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的记录。  
  
 SqlXmlAdapter 对象支持这些构造函数：  
  
```  
public SqlXmlAdapter(SqlXmlCommand  cmd)   
  
public SqlXmlAdapter(  
                     string commandText,   
                     SqlXmlCommandType cmdType,   
                     string connectionString  
                      )   
  
public SqlXmlAdapter(  
                     Stream commandStream,   
                     SqlXmlCommandType cmdType,   
                     string connectionString  
                     )   
```  
  
## <a name="see-also"></a>另请参阅  
 [SqlXmlCommand 对象 & #40;SQLXML 托管类 & #41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmlcommand-object.md)   
 [SqlXmlParameter 对象 & #40;SQLXML 托管类 & #41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmlparameter-object.md)  
  
  
