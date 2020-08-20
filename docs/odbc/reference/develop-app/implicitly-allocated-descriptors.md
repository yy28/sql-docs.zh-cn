---
description: 隐式分配的描述符
title: 隐式分配的描述符 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- implicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 9f88c863-affc-4ab4-a558-63a3ef766f37
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5daa7f622798e1394c186b333069933b48e367af
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461419"
---
# <a name="implicitly-allocated-descriptors"></a>隐式分配的描述符
当分配语句句柄时，应用程序会隐式分配一组四个说明符。 应用程序可以获取这些隐式分配的描述符的句柄作为语句句柄的特性。 当应用程序释放语句句柄时，驱动程序将释放该句柄上的所有隐式分配的说明符。
