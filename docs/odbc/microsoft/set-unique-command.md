---
title: SET UNIQUE 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 29598ed97cba8be04a0c08727cffc40e663becba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063607"
---
# <a name="set-unique-command"></a>SET UNIQUE 命令
指定是否在索引文件中维护具有重复索引键值的记录。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 指定在索引文件中不包含重复的索引键值的任一记录。 仅具有原始索引键值的第一个记录包含在索引文件。  
  
 OFF  
 （默认值）。指定在索引文件中包含具有重复索引键值的记录。  
  
## <a name="remarks"></a>备注  
 在发出重新编制索引时，索引文件的唯一设置的设置将保留。 有关详细信息，请参阅[索引](../../odbc/microsoft/index-command.md)。
