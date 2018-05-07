---
title: 步骤 1： 配置用于 Node.js 开发的开发环境 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: node-js
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2dad01f1-fadf-4ac9-9b4d-26be3d301886
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 313adb458786f009cd2cbd4fa86c09d7d5302b29
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>步骤 1： 配置用于 Node.js 开发的开发环境
你将需要配置你的开发环境满足先决条件，以便开发应用程序使用的 SQL Server Node.js 驱动程序。  最常见方法是使用 node 程序包管理器 (npm) 安装需要很长时间的模块，但你可以下载此模块需要很长时间直接在[Github](https://github.com/pekim/tedious)如果你愿意。  
  
请注意，Node.js 驱动程序使用 TDS 协议，默认情况下，SQL Server 和 Azure SQL 数据库中启用。  这种方式无需任何其他配置。  
  
## <a name="windows"></a>Windows  
  
1. **安装 Node.js 运行时和 npm 包管理器**  
a. 转到[Node.js](https://nodejs.org/en/download/)  
b. 单击相应的 Windows installer msi 链接。   
c. 下载完成后，运行 msi 安装 Node.js  
  
2. **打开 cmd.exe**  
  
3. **创建项目目录**并导航到它。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **创建节点项目。**  若要在项目创建期间保留默认值，按 enter，直到创建项目。 在此步骤结束时，你应在你的项目目录中看到的 package.json 文件。  
```  
> npm init  
```  
  
5. **在项目中安装需要很长时间的模块。**  这是该驱动程序用于与 SQL Server 进行通信的 TDS 协议的实现。  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **打开终端**  
  
2. **安装 Node.js 运行时**  
```  
>sudo apt-get install node  
```  
3. **安装 npm （node 包管理器）**  
```  
> sudo apt-get install npm  
```  
4. **创建项目目录**并导航到它。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **创建节点项目。**  若要在项目创建期间保留默认值，按 enter，直到创建项目。 在此步骤结束时，你应在你的项目目录中看到的 package.json 文件。  
```  
> sudo npm init  
```  
  
6. **在项目中安装需要很长时间的模块。**  这是该驱动程序用于与 SQL Server 进行通信的 TDS 协议的实现。  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **安装 Node.js 运行时和 npm 包管理器**  
a. 转到[Node.js](https://nodejs.org/en/download/)  
b. 单击相应的 Mac OS 安装程序链接。  
c. 下载完成后，运行 dmg 安装 Node.js  
  
2. **打开终端**  
  
3. **创建项目目录**并导航到它。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **创建节点项目。**  若要在项目创建期间保留默认值，按 enter，直到创建项目。 在此步骤结束时，你应在你的项目目录中看到的 package.json 文件。  
```  
> npm init  
```  
  
5. **在项目中安装需要很长时间的模块。**  这是该驱动程序用于与 SQL Server 进行通信的 TDS 协议的实现。  
```  
> npm install tedious  
```  
  
