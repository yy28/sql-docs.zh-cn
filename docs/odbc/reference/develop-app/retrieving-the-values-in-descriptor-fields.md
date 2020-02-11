---
title: 检索描述符字段中的值 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: c05b180f-c2b0-437b-8d1c-ce7f4da93287
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 55d7017c659ca4d0b8094ed4a665d27c10b355f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020456"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>检索描述符字段中的值
应用程序可以调用**SQLGetDescField**来获取描述符记录的单个字段。 **SQLGetDescField**使应用程序可以访问在 ODBC 中定义的所有描述符字段，还可以访问驱动程序定义的字段。  
  
 可以调用**SQLGetDescRec**来检索影响列或参数数据的数据类型和存储的多个描述符字段的设置。
