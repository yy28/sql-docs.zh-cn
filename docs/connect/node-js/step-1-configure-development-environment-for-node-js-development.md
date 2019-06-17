---
title: 步骤 1：配置用于 Node.js 开发的开发环境 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2dad01f1-fadf-4ac9-9b4d-26be3d301886
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 49522e397789c5193ed8f218a5fdf776ba62f001
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799359"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>步骤 1：配置用于 Node.js 开发的开发环境
你将需要在满足先决条件配置开发环境，以便开发使用 Node.js Driver for SQL Server 的应用程序。  最常见方法是使用节点包管理器 (npm) 安装枯燥乏味的模块，但可以在下载单调乏味模块直接在[Github](https://github.com/pekim/tedious)您的喜好而定。  
  
请注意，Node.js 驱动程序使用 SQL Server 和 Azure SQL 数据库中的默认情况下启用的 TDS 协议。  这种方式无需任何其他配置。  
  
## <a name="windows"></a>Windows  
  
1. **安装 Node.js 运行时和 npm 程序包管理器**  
A. 转到[Node.js](https://nodejs.org/en/download/)  
B. 单击相应的 Windows 安装程序 msi 链接。   
c. 下载完成后，运行 msi 安装 Node.js  
  
2. **打开 cmd.exe**  
  
3. **创建项目目录**并导航到它。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **创建节点项目。**  若要在项目创建期间保留默认值，按 enter，直到创建项目。 在此步骤结束时，你应在项目目录中看到一个 package.json 文件。  
```  
> npm init  
```  
  
5. **在项目中安装枯燥乏味的模块。**  这是驱动程序使用与 SQL Server 进行通信的 TDS 协议的实现。  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **打开终端**  
  
2. **安装 Node.js 运行时**  
```  
>sudo apt-get install node  
```  
3. **安装 npm （节点包管理器）**  
```  
> sudo apt-get install npm  
```  
4. **创建项目目录**并导航到它。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **创建节点项目。**  若要在项目创建期间保留默认值，按 enter，直到创建项目。 在此步骤结束时，你应在项目目录中看到一个 package.json 文件。  
```  
> sudo npm init  
```  
  
6. **在项目中安装枯燥乏味的模块。**  这是驱动程序使用与 SQL Server 进行通信的 TDS 协议的实现。  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **安装 Node.js 运行时和 npm 程序包管理器**  
A. 转到[Node.js](https://nodejs.org/en/download/)  
B. 单击相应的 Mac OS 安装程序链接。  
c. 下载后，运行 dmg 安装 Node.js  
  
2. **打开终端**  
  
3. **创建项目目录**并导航到它。    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **创建节点项目。**  若要在项目创建期间保留默认值，按 enter，直到创建项目。 在此步骤结束时，你应在项目目录中看到一个 package.json 文件。  
```  
> npm init  
```  
  
5. **在项目中安装枯燥乏味的模块。**  这是驱动程序使用与 SQL Server 进行通信的 TDS 协议的实现。  
```  
> npm install tedious  
```  
  
