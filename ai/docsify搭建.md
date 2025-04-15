以下是搭建Docsify文档站点的详细教程，结合了最新实践和常见配置方案：

### 一、环境准备
1. 安装Node.js（需12.x或更高版本）
2. 确保npm/yarn可用（Node.js自带）

### 二、基础安装
```bash
npm install -g docsify-cli  # 全局安装CLI工具
docsify init ./docs        # 初始化项目
docsify serve docs         # 启动本地服务（默认端口3000）
```

### 三、核心文件结构
```
docs/
├── index.html    # 主配置文件
├── README.md     # 默认主页内容
└── .nojekyll     # 防止GitHub Pages忽略下划线文件
```

### 四、常用配置（修改index.html）
```html
<script>
window.$docsify = {
  name: '项目名称',
  repo: 'https://github.com/your-repo',
  loadSidebar: true,      // 启用侧边栏
  subMaxLevel: 2,         // 侧边栏层级深度
  search: 'auto',         // 启用搜索
  coverpage: true         // 启用封面页
}
</script>
```

### 五、进阶功能
1. **侧边栏配置**  
   创建`_sidebar.md`文件：
   ```markdown
   - [首页](README.md)
   - [第一章](part1/README.md)
     - [1.1节](part1/section1.md)
   ```

2. **封面页配置**  
   创建`_coverpage.md`：
   ```markdown
   ![logo](_media/icon.svg)
   # 项目名称
   > 项目描述
   [开始阅读](#README)
   ```

3. **插件扩展**  
   • 代码高亮：添加Prism.js
   • LaTeX支持：引入Katex
   • 字数统计：使用docsify-count

### 六、部署方案
1. **GitHub Pages**  
   将docs目录推送到仓库，在Settings > Pages中选择分支和docs目录

2. **Nginx部署**  
   ```nginx
   server {
     listen 80;
     root /var/www/docsify;
     index index.html;
     location / {
       try_files $uri /index.html;
     }
   }
   ```

3. **内网穿透**  
   使用cpolar工具实现公网访问（适合本地调试）

### 注意事项
• 所有Markdown文件需使用UTF-8编码
• 自定义样式可通过修改`index.html`引入CSS文件
• 遇到`docsify`命令找不到时，检查Node.js的bin目录是否在PATH中

官方文档参考：[Docsify官网](https://docsify.js.org/)
***
# 我的Docsify配置

## index.html
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>5m笔记</title>
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
    <meta name="description" content="Description">
    <meta name="viewport"
        content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <!-- 设置浏览器图标 -->
    <link rel="icon" href="/favicon.ico" type="image/x-icon" />
    <link rel="shortcut icon" href="/favicon.ico" type="image/x-icon" />
    <!-- 默认主题 -->
    <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify/lib/themes/vue.css">
</head>

<body>
    <!-- 定义加载时候的动作 -->
    <div id="app">加载中...</div>
    <script>
        window.$docsify = {
            // 项目名称
            name: '5m笔记',
            // 仓库地址，点击右上角的Github章鱼猫头像会跳转到此地址
            repo: 'https://github.com/nilinseo/5m',
            // 侧边栏支持，默认加载的是项目根目录下的_sidebar.md文件
            loadSidebar: true,
            // 导航栏支持，默认加载的是项目根目录下的_navbar.md文件
            loadNavbar: true,
            // 封面支持，默认加载的是项目根目录下的_coverpage.md文件
            coverpage: true,
            // 最大支持渲染的标题层级
            maxLevel: 5,
            // 自定义侧边栏后默认不会再生成目录，设置生成目录的最大层级（建议配置为2-4）
            subMaxLevel: 4,
            // 小屏设备下合并导航栏到侧边栏
            mergeNavbar: true,
            /*搜索相关设置*/
            search: {
                maxAge: 86400000,// 过期时间，单位毫秒，默认一天
                paths: 'auto',// 注意：仅适用于 paths: 'auto' 模式
                placeholder: '搜索',              
                // 支持本地化
                placeholder: {
                    '/zh-cn/': '搜索',
                    '/': 'Type to search'
                },
                noData: '找不到结果',
                depth: 4,
                hideOtherSidebarContent: false,
                namespace: '5m笔记',
            }
        }
    </script>
    <!-- docsify的js依赖 -->
    <script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
    <!-- emoji表情支持 -->
    <script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/emoji.min.js"></script>
    <!-- 图片放大缩小支持 -->
    <script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/zoom-image.min.js"></script>
    <!-- 搜索功能支持 -->
    <script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/search.min.js"></script>
    <!--在所有的代码块上添加一个简单的Click to copy按钮来允许用户从你的文档中轻易地复制代码-->
    <script src="//cdn.jsdelivr.net/npm/docsify-copy-code/dist/docsify-copy-code.min.js"></script>
</body>

</html>
```

