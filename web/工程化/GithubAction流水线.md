<!--
 * @Author: 夏朝辉 lesslessmore@163.com
 * @Date: 2023-05-30 14:38:00
 * @LastEditors: 夏朝辉 lesslessmore@163.com
 * @LastEditTime: 2023-05-30 14:48:27
-->
# CI/CD Github Action流水线

产品开发的完整生命周期一般可划分为几个不同的阶段：

- Plan：计划
- Code：开发
- Build：构建
- Test：测试
- Release：发布
- Deploy：部署
- Operate：运维
- Monitor：措施，持续反馈，形成一个闭环

![Untitled](/assets/web/工程化/CICD.png)

# CICD

**CI，Continuous Integration**，**持续集成**，是指在**开发过程中，持续的将开发者编写的代码多次的合并到主干上**。**开发人员每次提交代码之后，都会触发自动构建和测试，以尽快发现问题**。如果测试通过，则将新代码合并到主干上。如果测试失败，则反馈给开发人员，进行bug的修复。

**CD**是 **Continuous Delivery 持续交付**和 **Continuous Deploy 持续部署**的简称。

持续交付是指在**完成 CI 中的自动化构建和测试之后，自动将代码发布到存储库。**也就是说，持续交付的目的是**生成一套可随时部署到生产环境的代码。**
持续部署则是持续交付的延伸，是指**自动化的将代码部署到生产环境中。**

# Github Actions

GitHub Action由微软推出，是一个持续集成和持续交付 (CI/CD) 平台，可用于自动执行构建、测试和部署管道，帮助实现开发工作流的自动化。

## 特点

- 多平台
- 多语言
- 矩阵构建
- 实时日志
- 多容器测试
- 社区支持

费用

在GitHub上托管的开源仓库免费使用，私有仓库每月可享有 2000分钟到50000分钟的免费时长，超出后会收费

## 核心概念

### workFlow工作流

工作流是一种可配置的**自动化过程**，会运行一个或多个Jobs，用于完成一项或多项工作，通过`YAML`配置来定义。

可以将其理解为**完成一次CI / CD的过程。**

在仓库中`.github/workflows`目录下创建`YAML`格式的配置文件，在`YAML`配置文件中定义工作流。

配置文件的名字可以自定义，没有特殊要求。

可以创建多个`YAML`文件来执行不同的任务集。

### event事件

在配置文件中通过`on`属性来指定工作流执行的时机。

可在仓库中的事件触发时运行，也可以手动触发，或使用定时器触发。

常用的[仓库事件](https://docs.github.com/cn/actions/using-workflows/events-that-trigger-workflows)例如push、delete等

### job任务

一个工作流通常由一个或多个`jobs`（任务集）组成，默认情况下任务集并行运行。一个任务集可包含多个`job`（任务），每个任务都需要指定一个任务id。

job是Step的集合，一个job包含若干个Steps，每个Steps可以是将被执行的Shell命令或脚本

### runner运行器

自动化构建、测试的虚拟机环境runner运行器是指将在工作流程中处理作业的计算机类型。

每个job任务运行在自己的虚拟机runner或者容器中，一个job中的若干个steps可以共享数据。但是jobs之间是相互隔离的，数据不共享。

在job任务中通过`runs-on`来定义该任务运行的虚拟机环境（操作系统），其可以是 GitHub 托管的运行器，也可以是自托管运行器。

GitHub提供的[常用的虚拟机环境](https://docs.github.com/cn/actions/using-jobs/choosing-the-runner-for-a-job#%E9%80%89%E6%8B%A9-github-%E6%89%98%E7%AE%A1%E7%9A%84%E8%BF%90%E8%A1%8C%E5%99%A8)有Ubuntu、Windows Server和MacOS等，选择的对应虚拟机称作runner运行器。

如果使用 GitHub 托管的运行器，每个任务将在`runs-on`指定的运行器映像的新实例中运行。

### step步骤

一个任务内的具体工作由step来指定，steps是一组由多个step分步步骤组成的集合。

一个执行步骤可以是一个shell命令，也可以是一个具体的action动作。

### action动作

`ction`是一种可重复使用的代码单位，即封装的一些需要频繁使用的任务，目的是用来简化workflow。

常用的[action](https://github.com/marketplace?query=)有拉取仓库代码供后续步骤使用的`checkout`等。

## 配置action secret密钥

在工作流配置文件中会使用到要部署的服务器地址和密码等信息，明文传输很不安全，可以选择将此类敏感信息保存为加密后的环境变量，在工作流配置文件中通过变量`${{ 变量名 }}`的形式调用。

配置位置：仓库的settings > Secrets > Actions

点击`New respository secret`按钮，输入服务器IP、用户、密码等相关信息创建变量

![Untitled](/assets/web/工程化/actionWorkflow1.png)

## 工作流配置文件

在项目根目录创建`.github/workflows`文件夹，新建一个.yml文件，文件名自定义即可，填写配置信息，然后推送到仓库中。

```yaml
# 流程名称
name: Github Action CI

on:
 # 监听master分支的push事件，触发流程
  push:
    branches: ['master']
  pull_request:
    branches: ['master']

jobs:
  # job任务的ID名：start-action-build
  start-action-build:
    # 指定任务job执行的运行器。latest 表示是 GitHub 提供的最新稳定映像，但可能不是操作系统供应商提供的最新版本。
    runs-on: ubuntu-latest

    # 定义job任务的具体步骤
    steps:
      # 子步骤1：从仓库拉取代码到Runner里的操作
      - name: Checkout repository
        # 第三方的action：从Github仓库中checkout代码到Github Actions的运行器中使用
        uses: actions/checkout@v3

      # 子步骤1：安装指定版本的 Node.js，此处指定安装的版本为v14
      - name: Use Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '14'

      # 子步骤2：安装依赖
      - name: Installing Dependencies
        run: npm install

      # 子步骤3：打包构建项目
      - name: Building Project
        run: npm run build

      # 子步骤4：执行部署任务
      - name: Deploy to Server
        uses: cross-the-world/ssh-scp-ssh-pipelines@latest
        with:
          cache: 'npm'
          host: ${{ secrets.SERVER_HOST }}
          user: ${{ secrets.SERVER_USER }}
          pass: ${{ secrets.SERVER_PASS }}

          connect_timeout: 60s

     # 使用scp命令向其他服务器传输某文件到某位置
          scp: |
            ./build => /home/xiachaohui
```

字段解释

- name：流程的名称
- on：触发的事件
- runs-on：指定运行的Runner
- steps：任务重包含的步骤
- uses：使用某个action
- run：执行某个shell命令或脚本
- with：指定需要传入的参数

## 自动化部署项目

代码推送后，监听到触发的push事件，开始自动化部署任务。

开始运行自动化流程：

![Untitled](/assets/web/工程化/actionWorkflow1.png)

![Untitled](/assets/web/工程化/actionWorkflow2.png)

![Untitled](/assets/web/工程化/actionWorkflow3.png)

至此，流程部署完毕，撒花🎉🎉🎉
