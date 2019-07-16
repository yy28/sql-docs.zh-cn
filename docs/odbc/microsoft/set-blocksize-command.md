---
title: SET BLOCKSIZE 命令 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set blocksize command [ODBC]
ms.assetid: 0c11580f-37f5-4a8e-99be-9fb9c44bb433
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4fe84a470f5e877c73701168394cd85d75253fb7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997757"
---
# <a name="set-blocksize-command"></a>SET BLOCKSIZE 命令
指定如何为备注字段的存储分配磁盘空间。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>参数  
 *nBytes*  
 指定在其中分配磁盘空间的备注字段的块大小。 如果*nBytes*为 0，则用单字节 （1 个字节的块） 分配的磁盘空间。 如果*nBytes*是介于 1 和 32，磁盘空间之间的整数中的块分配*nBytes*乘以 512 个字节。 如果*nBytes*大于 32，在的块中分配的磁盘空间*nBytes*字节。 如果指定的块大小值大于 32，可以节省大量磁盘空间。  
  
## <a name="remarks"></a>备注  
 设置块大小的默认值为 64。 重置的块大小为不同的值，在创建该文件后，将其设置为新值，然后使用复制以创建新表。 新的表具有指定的块大小。
