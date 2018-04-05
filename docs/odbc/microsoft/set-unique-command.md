---
title: SET 唯一命令 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SET UNIQUE command [ODBC]
ms.assetid: 1f69e31e-4599-47cc-ac89-b86fba8703c5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0ba0921d2bfab8911d129ac4d1430e6d8d9bd6fe
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="set-unique-command"></a>SET 唯一命令
指定是否具有重复的索引键值的记录保留在索引文件。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 指定在索引文件中不包含具有重复的索引键值的任何记录。 仅具有原始索引键值的第一个记录包含在索引文件。  
  
 OFF  
 （默认值。）指定在索引文件中包含具有重复的索引键值的记录。  
  
## <a name="remarks"></a>Remarks  
 当发出重新编制索引时，索引文件将保留其唯一设置的设置。 有关详细信息，请参阅[索引](../../odbc/microsoft/index-command.md)。
