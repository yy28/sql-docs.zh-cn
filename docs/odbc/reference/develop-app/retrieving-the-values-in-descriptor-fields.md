---
description: 检索描述符字段中的值
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a2118efe58b076287dd75192de679bdb74299435
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494645"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>检索描述符字段中的值
应用程序可以调用 **SQLGetDescField** 来获取描述符记录的单个字段。 **SQLGetDescField** 使应用程序可以访问在 ODBC 中定义的所有描述符字段，还可以访问驱动程序定义的字段。  
  
 可以调用**SQLGetDescRec**来检索影响列或参数数据的数据类型和存储的多个描述符字段的设置。
