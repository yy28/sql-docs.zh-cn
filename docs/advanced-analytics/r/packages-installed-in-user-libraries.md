---
title: "用户库中安装的包 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 99ffd9b8-aa6d-4ac2-9840-4e66d0463978
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b4d5c7f3d1d0da5e1967140fcbdfcf60ba4571e7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="packages-installed-in-user-libraries"></a>用户库中安装的包

如果非管理员用户需要新的 R 包，则这些包不能安装到默认位置，而是默认情况下安装到专用的用户库。 

在典型的 R 开发环境中，若要在代码中引用包，用户必须将位置添加到 R 环境变量 `libPath` 中，或者引用完整的包路径，如下所示：  
  
~~~~
library("c:/Users/<username>/R/win-library/packagename")  
~~~~

## <a name="problems-with-packages-in-user-libraries"></a>用户库中的包存在的问题

但是，在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中，**不**支持此解决方法；必须将包安装到默认库。 如果包未安装到默认库中，则在尝试调用该包时，可能会收到以下错误：

*库(xxx)中出错: 没有名为 'xxx' 的包*
 

因此，当你迁移 R 解决方案以在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中运行时，请务必执行以下操作：
+ 将所需的任何包安装到默认库。
+ 编辑代码以确保从默认库（而不是从临时目录或用户库）加载包。
+ 检查代码以确保未调用已卸载的包。
+ 修改会尝试动态安装包的任何代码。
 
如果包安装在默认库中，则 R 运行时将从默认库加载包，即使 R 代码中指定了不同的库也是如此。

## <a name="see-also"></a>另请参阅
