---
title: 保留分层记录集 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO], persisting
- persisting hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 43798bb5-98a6-4ad6-9bf8-78154b3a1827
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 281204b15620eba99f30c4480817973052af0cea
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38980953"
---
# <a name="persisting-hierarchical-recordsets"></a>保留分层记录集
您可以将保存的分层**记录集**中通过调用 ADTG 或 XML 格式的文件[保存](../../../ado/reference/ado-api/save-method.md)方法。 但是，两个限制应用保存层次结构时**记录集**以 XML 格式的 s： 如果，则不能保存在 XML 中的层次结构**记录集**包含挂起的更新，且不能保存参数化分层**记录集**。  
  
 有关定型数据提供程序的详细信息，请参阅[适用于 OLE DB 的 Microsoft Data Shaping 服务](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)(ADO) 和[OLE DB Data Shaping 服务的概述](http://msdn.microsoft.com/9f51e471-8e85-448e-9fb8-b64bbf767bf3)。  
  
## <a name="see-also"></a>请参阅  
 [数据整理示例](../../../ado/guide/data/data-shaping-example.md)   
 [正式 Shape 语法](../../../ado/guide/data/formal-shape-grammar.md)   
 [常用 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
