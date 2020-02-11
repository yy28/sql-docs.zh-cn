---
title: 修改对二进制大型对象（Blob）进行读写的 UPDATETEXT 语句 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- UPDATETEXT statement
- text [SQL Server], UPDATETEXT statements
ms.assetid: b85da6a7-42f6-4707-a25e-3ded8958b94f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f2f3c8af333cc20398e7951bd6fd53433da0288c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093764"
---
# <a name="modify-updatetext-statements-that-read-and-write-to-binary-large-objects-blobs"></a>修改读写到二进制大型对象(BLOB)的 UPDATETEXT 语句
  升级顾问检测到 UPDATETEXT 语句使用同一文本指针读写相同的二进制大型对象 (BLOB)。 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 不支持以这种方式使用文本指针。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>纠正措施  
 请将 BLOB 复制到一个临时表或表变量，然后将值赋回给原始列。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
