# 在Vercel上部署Twikoo评论系统指南

## 前言

本指南将帮助您在Vercel平台上部署Twikoo评论系统，并将其集成到您的网站中。Twikoo是一个简洁、安全的评论系统，基于腾讯云开发。通过Vercel部署，您可以免费获得一个稳定的评论服务。

## 准备工作

1. 一个GitHub账号
2. 一个Vercel账号（可以直接使用GitHub账号登录）

## 部署步骤

### 1. 创建GitHub仓库

1. 登录您的GitHub账号
2. 点击右上角的"+"按钮，选择"New repository"
3. 填写仓库名称，例如"twikoo-vercel"
4. 选择公开(Public)或私有(Private)，这不影响功能
5. 点击"Create repository"创建仓库

### 2. 导入Twikoo模板

有两种方法可以导入Twikoo模板：

#### 方法一：直接从Vercel导入（推荐）

1. 访问Twikoo官方的Vercel部署链接：https://vercel.com/import/project?template=https://github.com/imaegoo/twikoo/tree/dev/src/server
2. 使用GitHub账号登录Vercel（如果尚未登录）
3. 输入一个项目名称，例如"twikoo-comments"
4. 点击"Deploy"开始部署

#### 方法二：手动克隆并推送

1. 克隆Twikoo仓库到本地：
   ```bash
   git clone https://github.com/imaegoo/twikoo.git
   ```
2. 进入服务端目录：
   ```bash
   cd twikoo/src/server
   ```
3. 将此目录关联到您的GitHub仓库：
   ```bash
   git init
   git remote add origin https://github.com/您的用户名/twikoo-vercel.git
   ```
4. 提交并推送代码：
   ```bash
   git add .
   git commit -m "Initial commit"
   git push -u origin main
   ```

### 3. 在Vercel上部署

如果您使用了方法一，Vercel会自动开始部署。如果使用方法二，请按以下步骤操作：

1. 登录Vercel：https://vercel.com/
2. 点击"New Project"
3. 在"Import Git Repository"部分，找到并选择您刚才创建的仓库
4. 保持默认设置，点击"Deploy"开始部署

### 4. 获取环境ID

部署完成后，Vercel会提供一个域名，格式类似：`https://your-project-name.vercel.app`

这个域名就是您的Twikoo环境ID，请记录下来。

## 集成到网站

现在，您需要将部署好的Twikoo服务集成到您的网站中。

### 修改detail.html文件

打开`templates/detail.html`文件，找到Twikoo初始化代码，将环境ID替换为您刚才获取的Vercel域名：

```javascript
twikoo.init({
    envId: 'https://your-project-name.vercel.app', // 替换为您的Vercel域名
    el: '#twikoo',
    // 可选配置
    region: '', // 环境地域，默认为 ap-shanghai
    path: '{{ post.record_id }}', // 用文章ID作为评论页面的唯一标识
});
```

## 验证部署

1. 启动您的网站
2. 访问任意文章页面
3. 滚动到页面底部，查看评论区是否正常加载
4. 尝试发表评论测试功能是否正常

## 常见问题

### 评论区无法加载

- 检查浏览器控制台是否有错误信息
- 确认环境ID是否正确填写
- 确认Vercel部署是否成功

### 评论提交失败

- 检查网络连接
- 确认Vercel服务是否正常运行
- 尝试清除浏览器缓存后重试

### 部署失败问题

如果在Vercel部署过程中遇到"Deployment Preparing Git Repository..."阶段的错误提示："An unexpected error occurred"，可以尝试以下解决方案：

1. 检查GitHub权限
   - 确保您已经正确授权Vercel访问您的GitHub仓库
   - 在Vercel的设置中重新连接GitHub账号

2. 清理缓存并重试
   - 在Vercel控制台中删除该项目
   - 清除浏览器缓存
   - 重新从头开始导入项目

3. 使用手动部署方式
   - 如果自动导入持续失败，建议使用上述的"方法二：手动克隆并推送"的方式
   - 手动将代码推送到GitHub后再在Vercel中导入

4. 检查仓库状态
   - 确保GitHub仓库已成功创建
   - 验证仓库权限设置是否正确
   - 检查仓库是否包含必要的Twikoo源代码

如果以上方法都无法解决，建议：
- 等待几分钟后再次尝试
- 查看Vercel的状态页面是否有服务中断报告
- 通过Vercel的支持渠道寻求帮助

## 高级配置

### 自定义域名

如果您希望使用自己的域名而不是Vercel提供的域名，可以在Vercel项目设置中添加自定义域名：

1. 在Vercel控制台中选择您的Twikoo项目
2. 点击"Settings" > "Domains"
3. 添加您的自定义域名并按照指引完成DNS配置

### 评论管理

首次使用时，系统会自动将第一个评论者设为管理员。管理员可以：

1. 登录后台管理评论
2. 设置评论审核
3. 导入导出数据

访问`https://your-project-name.vercel.app/ui`进入管理界面。

## 结语

现在您已经成功部署了Twikoo评论系统，并将其集成到您的网站中。如果遇到任何问题，可以参考[Twikoo官方文档](https://twikoo.js.org/)或在GitHub上提交issue。