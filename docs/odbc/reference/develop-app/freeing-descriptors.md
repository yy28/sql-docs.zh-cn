---
title: 释放描述符 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
- descriptors [ODBC], allocating and freeing
- freeing descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 317213f4-0ebb-4bf8-a37a-4d6b1313823f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: af30ceb29e032764b89aa2069086aa898a7d35db
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305598"
---
# <a name="freeing-descriptors"></a>释放描述符
显式分配的描述符可以通过以下方式释放：使用*HandleType*的 SQL_HANDLE_DESC 调用**SQLFreeHandle** ，或在释放连接句柄时隐式释放。 释放显式分配的描述符后，所应用的已释放说明符的所有语句句柄都会自动还原为为它们隐式分配的说明符。  
  
 隐式分配的描述符只能通过调用**SQLDisconnect**来释放，后者会删除在连接上打开的任何语句或说明符，或通过使用 SQL_HANDLE_STMT 的*HandleType*调用**SQLFreeHandle**来释放语句句柄和与该语句关联的所有隐式分配的说明符。 不能通过使用 SQL_HANDLE_DESC 的*HandleType*调用**SQLFreeHandle**来释放隐式分配的描述符。  
  
 即使在释放时，隐式分配的描述符仍有效，并且可以对其字段调用**SQLGetDescField** 。
