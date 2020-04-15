---
title: 设置重新处理命令 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET REPROCESS command [ODBC]
ms.assetid: b0708757-b1d7-42f3-8988-787f2a806b8b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5a7eb5fd19ca538c4f25077926567011ae133e54
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300827"
---
# <a name="set-reprocess-command"></a>SET REPROCESS 命令
指定在锁定尝试失败后锁定文件或记录的次数或时间。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET REPROCESS TO nAttempts [SECONDS] | TO AUTOMATIC  
```  
  
## <a name="arguments"></a>参数  
 到*n 次尝试*[秒]  
 指定在初始尝试失败后尝试锁定记录或文件的次数或秒数。 默认值为 0;最大值为 32，000。  
  
 SECONDS 指定 Visual FoxPro 尝试锁定文件或记录，但时间*为 n，时间*数秒。 仅当*n 次次次次*大于零时，它才可用。  
  
 例如，如果*nATos*为 30，Visual FoxPro 会尝试锁定记录或文件最多 30 次。 如果您还包括 SECONDS（SET REPROCESS 到 30 秒），Visual FoxPro 会不断尝试锁定记录或文件长达 30 秒。  
  
 如果 ON ERROR 例程有效，并且命令锁定记录或文件的尝试不成功，则执行 ON ERROR 例程。 但是，如果函数尝试锁定，则不会执行 ON ERROR 例程，并且函数返回 False （）。F.）。  
  
 如果 ON ERROR 例程无效，命令将尝试锁定记录或文件，并且无法放置锁，则生成错误。 如果函数尝试放置锁，则不显示警报，并且函数返回 False （）。F.）。  
  
 如果*nTries*为 0（默认值），并且您发出一个命令或函数，尝试锁定记录或文件，Visual FoxPro 将尝试无限期锁定记录或文件。 如果等待时记录或文件可用于锁定，则锁定并清除系统消息。 如果函数尝试放置锁，则函数返回 True （。T.）。  
  
 如果 ON ERROR 例程有效，并且命令尝试锁定记录或文件，则 ON ERROR 例程优先于锁定记录或文件的其他尝试。 立即执行 ON ERROR 例程。 Visual FoxPro 不会尝试其他记录或文件锁，也不会显示系统消息。  
  
 如果*nATos*为 1，Visual FoxPro 会尝试无限期锁定记录或文件，并且不会执行 ON ERROR 例程。  
  
 如果其他用户已在您尝试锁定的记录或文件中放置了锁，则必须等待用户释放锁。  
  
 到自动  
 指定 Visual FoxPro 尝试无限期锁定记录或文件。 （将 REPROCESS 设置为 -2 是等效命令。  
  
## <a name="remarks"></a>备注  
 首次尝试锁定记录或文件并不总是成功的。 通常，记录或文件被网络上的其他用户锁定。 SET REPROCESS 确定 Visual FoxPro 在初始尝试不成功时是否进行了其他尝试来锁定记录或文件。 您可以指定进行额外尝试的次数或尝试的时间。 ON ERROR 例程会影响处理不成功的锁尝试的方式。
