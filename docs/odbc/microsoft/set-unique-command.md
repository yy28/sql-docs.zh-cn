---
description: SET UNIQUE 命令
title: 设置唯一命令 |Microsoft Docs
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
ms.openlocfilehash: b8fa4ca11ed5beae08bfcbeb8b5a55d6c2969785
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412453"
---
# <a name="set-unique-command"></a>SET UNIQUE 命令
指定是否在索引文件中维护具有重复索引键值的记录。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 指定包含重复索引键值的任何记录均不包含在索引文件中。 索引文件中仅包含具有原始索引键值的第一条记录。  
  
 OFF  
  (默认值。 ) 指定索引文件中包含具有重复索引键值的记录。  
  
## <a name="remarks"></a>备注  
 发出索引编制时，索引文件会保留其唯一设置。 有关详细信息，请参阅 [INDEX](../../odbc/microsoft/index-command.md)。
