---
title: 设置独立命令 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET UNIQUE command [ODBC]
ms.assetid: 1f69e31e-4599-47cc-ac89-b86fba8703c5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7d3d37509450d1305891100b37bfd1ad026166e8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300837"
---
# <a name="set-unique-command"></a>SET UNIQUE 命令
指定索引文件中是否保留具有重复索引键值的记录。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 指定索引文件中不包括任何具有重复索引键值的记录。 索引文件中仅包含具有原始索引键值的第一个记录。  
  
 OFF  
 （默认值。指定索引文件中包含具有重复索引键值的记录。  
  
## <a name="remarks"></a>备注  
 当您发出 REINDEX 时，索引文件将保留其"设置唯一"设置。 有关详细信息，请参阅[INDEX](../../odbc/microsoft/index-command.md)。
