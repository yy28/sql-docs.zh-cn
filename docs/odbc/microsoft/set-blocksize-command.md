---
description: SET BLOCKSIZE 命令
title: 设置区块命令 |Microsoft Docs
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
ms.openlocfilehash: 6677a397542f4bcd7f27b11cd032092b7087a9fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466389"
---
# <a name="set-blocksize-command"></a>SET BLOCKSIZE 命令
指定为备注字段的存储分配磁盘空间的方式。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>参数  
 *nBytes*  
 指定为备注字段分配的磁盘空间的块大小。 如果 *nBytes* 为0，则以单字节为单位分配磁盘空间)  (块。 如果 *nBytes* 是1到32之间的整数，则磁盘空间按 *nBytes* 字节的块进行分配，乘以512。 如果 *nBytes* 大于32，则将在 *nBytes* 字节的块中分配磁盘空间。 如果指定的块大小值大于32，可以节省大量磁盘空间。  
  
## <a name="remarks"></a>备注  
 SET 块大小的默认值为64。 若要在创建文件后将块大小重置为其他值，请将其设置为新值，然后使用 "复制" 创建新表。 新表具有指定的块大小。
