---
title: SqlXmlAdapter 对象 （SQLXML 托管类） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d657ba49f7d4905eef8eaa0bdc3ca4327852df6d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126462"
---
# <a name="sqlxmladapter-object-sqlxml-managed-classes"></a>SqlXmlAdapter 对象（SQLXML 托管类）
  此对象提供用于促进与 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 中的数据集进行交互的方法。 有关工作示例，请参阅[.NET 环境中访问 SQLXML 功能](accessing-sqlxml-functionality-in-the-net-environment.md)。  
  
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
  
## <a name="see-also"></a>请参阅  
 [SqlXmlCommand 对象&#40;SQLXML 托管类&#41;](sqlxml-4-0-net-framework-support-managed-classes.md)   
 [SqlXmlParameter 对象&#40;SQLXML 托管类&#41;](sqlxml-managed-classes-sqlxmlparameter-object.md)  
  
  