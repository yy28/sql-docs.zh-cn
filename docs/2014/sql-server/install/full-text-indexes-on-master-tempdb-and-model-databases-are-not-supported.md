---
title: 不支持对 master、 tempdb 和 model 数据库的全文索引 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- full-text indexes
ms.assetid: f7992965-42c1-4eb8-a7fb-afb38b67c740
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1d334a3626c11050418df3fae483f5b9029adeb4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015620"
---
# <a name="full-text-indexes-on-master-tempdb-and-model-databases-are-not-supported"></a>不支持对 master、tempdb 和 model 数据库建立全文检索
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允许对任何系统数据库建立全文检索。  
  
## <a name="description"></a>Description  
 在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中，支持对 master、tempdb 和 model 数据库建立全文索引。  
  
 在升级过程将删除任何全文目录在 master、 tempdb 和模型数据库。  
  
## <a name="see-also"></a>请参阅  
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  