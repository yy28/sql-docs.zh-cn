---
title: 验证 SQL Server Analysis Services 累积更新生成版本 |Microsoft Docs
ms.date: 07/11/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1da8384bb51360178e1735d13f6c6b706e8b7ff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62659054"
---
# <a name="verify-analysis-services-cumulative-update-build-version"></a>验证 Analysis Services 累积更新内部版本

从 SQL Server 2017 开始，Analysis Services 内部版本号和 SQL Server 数据库引擎内部版本号不匹配。 尽管 Analysis Services 和数据库引擎使用相同的安装程序，生成系统每次使用是独立的。

 在某些情况下，可能需要验证已应用累积更新 (CU) 生成包，以及 Analysis Services 组件已被更新。 可以通过比较的生成版本号为特定 CU 安装在计算机上的 Analysis Services 组件文件的生成版本号进行验证。

## <a name="verify-component-file-version"></a>验证组件文件版本

若要验证组件文件版本 

1. 转到[SQL Server 2017 内部版本](https://support.microsoft.com/help/4047329)。 
2. 在中**SQL Server 2017 累积更新 (CU) 生成**，单击**知识库编号**你想要验证的生成。
3. 在中**累积更新 SQL Server 2017 （）** 一文中，在**累积更新包信息**部分中，展开**累积更新包文件信息**.
4. 在中**SQL Server 2017 Analysis Services**表中，检查的文件版本**msmdsrv.exe**组件文件。 如果应用了 CU，文件版本号应与您的计算机上安装的 msmdsrv.exe 文件匹配。

## <a name="see-also"></a>另请参阅  

[安装 SQL Server 服务更新](../../database-engine/install-windows/install-sql-server-servicing-updates.md)  

[Microsoft SQL server 更新中心](https://msdn.microsoft.com/library/ff803383.aspx)
  
  
