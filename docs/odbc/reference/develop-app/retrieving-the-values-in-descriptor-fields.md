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
manager: craigg
ms.openlocfilehash: ae95160a11a965e47845726748c2b9449a819e8a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47775955"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>检索描述符字段中的值
应用程序可以调用**SQLGetDescField**获取单个字段的描述符记录。 **SQLGetDescField**向在 ODBC 中，定义的所有描述符字段和驱动程序定义的字段以及提供的应用程序访问权限。  
  
 **SQLGetDescRec**可以调用以检索多个会影响的数据类型的描述符字段的设置和存储的列或参数的数据。
