---
title: 不支持对 master、 tempdb 和 model 数据库的全文索引 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes
ms.assetid: f7992965-42c1-4eb8-a7fb-afb38b67c740
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 743c7153b034cf5e1267c6a0da1e585845800980
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095202"
---
# <a name="full-text-indexes-on-master-tempdb-and-model-databases-are-not-supported"></a>不支持对 master、tempdb 和 model 数据库建立全文检索
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允许对任何系统数据库建立全文检索。  
  
## <a name="description"></a>Description  
 在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中，支持对 master、tempdb 和 model 数据库建立全文索引。  
  
 在升级过程中删除在 master、 tempdb 和 model 数据库中的任何全文目录。  
  
## <a name="see-also"></a>请参阅  
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
