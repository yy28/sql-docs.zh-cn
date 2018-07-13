---
title: 运行存储的过程 (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [OLE DB], executing
- OLE DB, stored procedures
- SQL Server Native Client OLE DB provider, stored procedures
ms.assetid: c77d9be9-2176-4438-8c7a-04b63ebece08
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9d1b2470c5d75a6a161459c615a093e0cfd83fc9
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37425047"
---
# <a name="running-stored-procedures-ole-db"></a>运行存储过程 (OLE DB)
  执行语句时，可以提供对数据源 （而不是执行或准备客户端应用程序中的语句直接） 调用存储的过程：  
  
-   提高性能。  
  
-   降低网络开销。  
  
-   提供更好的一致性。  
  
-   提高准确性。  
  
-   增加功能。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口支持三种机制，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]存储的过程用于返回数据：  
  
-   该过程中的每个 SELECT 语句生成的结果集。  
  
-   过程可以通过输出参数返回数据。  
  
-   过程可以具有整数返回代码。  
  
 应用程序必须能够处理所有这些输出的存储过程。  
  
 在结果处理期间，不同的 OLE DB 访问接口返回输出参数和返回值的时间不同。 情况下[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序、 输出参数和返回代码不提供直到后使用者检索或取消存储过程返回的结果集。 返回代码和输出参数在最后一个来自服务器的 TDS 数据包中返回。  
  
 访问接口返回输出参数和返回值时，使用 DBPROP_OUTPUTPARAMETERAVAILABILITY 属性进行报告。 此属性位于 DBPROPSET_DATASOURCEINFO 属性集中。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口将 DBPROP_OUTPUTPARAMETERAVAILABILITY 属性设置为 DBPROPVAL_OA_ATROWRELEASE，以指示，在处理或释放结果集之前不返回返回代码和输出参数。  
  
## <a name="see-also"></a>请参阅  
 [存储过程](stored-procedures.md)  
  
  
