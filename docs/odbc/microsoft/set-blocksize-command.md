---
title: 设置块大小命令 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3eb9fbe9df90f7ddafebc6baa029164a578a6da3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300897"
---
# <a name="set-blocksize-command"></a>SET BLOCKSIZE 命令
指定如何为备忘录字段的存储分配磁盘空间。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>参数  
 *n 字节*  
 指定分配备忘录字段的磁盘空间的块大小。 如果*n 字节*为 0，则以单个字节（1 字节的块）分配磁盘空间。 如果*n 字节*是介于 1 和 32 之间的整数，则磁盘空间以 n*字节*块乘以 512 为单位分配。 如果*n 字节*大于 32，则以 n*字节*块分配磁盘空间。 如果指定块大小值大于 32，则可以节省大量磁盘空间。  
  
## <a name="remarks"></a>备注  
 SET BLOCKSIZE 的默认值为 64。 要在创建文件后将块大小重置为其他值，请将其设置为新值，然后使用 COPY 创建新表。 新表具有指定的块大小。
