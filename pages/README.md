# Amigos Supply Chain - 企业官网

宁波阿密格供应链有限公司官方网站

## 项目简介

这是一个采用原生 HTML/CSS/JavaScript 构建的专业企业官方网站，为宁波阿密格供应链有限公司提供在线展示和业务推广平台。网站支持中英文双语，全面响应式设计，适配各种设备。

## 公司介绍

**宁波阿密格供应链有限公司** (NINGBO AMIGOS SUPPLY CHAIN CO.,LTD.) 成立于2018年，是一家一级国际货运代理企业，拥有无船承运人资质(NVOCC)。公司专注于为客户提供海运、空运、跨境电商物流、报关仓储等一站式供应链解决方案。

## 主要功能

### 核心业务模块
- **海运进出口** - 全球整柜、拼箱、散杂货运输服务
- **空运服务** - 国际快递和航空货运
- **FBA物流** - 亚马逊FBA头程、海外仓储服务
- **拖车报关** - 专业拖车、报关清关、仓储配送
- **南美专线** - 巴西、智利、阿根廷等南美国家专线服务

### 网站特性
- ✅ 响应式设计 - 完美支持移动端、平板、桌面
- ✅ 双语支持 - 中文和英文完整版本
- ✅ 动画效果 - 基于 AOS 的滚动动画
- ✅ 轮播展示 - Swiper 图片轮播
- ✅ 表单功能 - 联系表单和在线咨询
- ✅ SEO优化 - 语义化 HTML 结构

## 技术栈

### 前端技术
- **HTML5** - 语义化标签
- **CSS3** - CSS变量、Flexbox、Grid布局
- **JavaScript (ES6+)** - 原生JavaScript，无框架依赖

### 第三方库
- [Swiper 8.x](https://swiperjs.com/) - 图片轮播
- [AOS 2.3.4](https://michalsnik.github.io/aos/) - 滚动动画
- [Font Awesome 6.4.0](https://fontawesome.com/) - 图标库

### 设计系统
- 主色调：紫色系 (#7b1fa2)
- 字体：Microsoft YaHei, PingFang SC
- 响应式断点：768px, 992px, 1200px

## 项目结构

```
amigos-supply/
├── index.html                    # 中文主页
├── indexen.html                  # 英文主页
├── about.html                    # 关于我们
├── service-sea.html              # 海运服务
├── service-air.html              # 空运服务
├── service-fba.html              # FBA物流
├── service-customs.html          # 报关仓储
├── service-southamerica.html     # 南美专线
├── news1.html                    # 资讯：冷链物流
├── news2.html                    # 资讯：亚马逊FBA
├── news3.html                    # 资讯：国际海运
├── css/
│   └── style.css                 # 主样式文件
├── js/
│   └── main.js                   # 主脚本文件
└── images/                       # 图片资源
```

## 快速开始

### 本地运行

1. 克隆项目
```bash
git clone https://github.com/chaihuasong/amigos-supply.git
cd amigos-supply
```

2. 直接打开 HTML 文件
```bash
# 使用默认浏览器打开
open index.html  # macOS
start index.html  # Windows
xdg-open index.html  # Linux
```

或使用本地服务器：
```bash
# 使用 Python
python -m http.server 8000

# 使用 Node.js http-server
npx http-server

# 然后访问 http://localhost:8000
```

### 部署

该项目为纯静态网站，可以部署到任何静态托管服务：

- **GitHub Pages**
- **Netlify**
- **Vercel**
- **阿里云 OSS**
- **腾讯云 COS**

## 主要文件说明

### HTML 页面
- `index.html` / `indexen.html` - 网站首页（中英文）
- `about.html` - 公司介绍和资质展示
- `service-*.html` - 各项业务服务详情页
- `news*.html` - 行业资讯和公司动态

### CSS 样式
- `css/style.css` - 包含所有样式定义，使用 CSS 变量管理主题色

### JavaScript
- `js/main.js` - 包含轮播初始化、菜单交互、表单处理等功能

## 功能特性

### 响应式导航
- 桌面端：横向导航栏 + 下拉菜单
- 移动端：汉堡菜单 + 抽屉导航

### 轮播展示
- 英雄横幅轮播（6.5秒自动切换）
- 合作伙伴展示（响应式多列）

### 交互功能
- 平滑滚动锚点跳转
- 返回顶部按钮（滚动>300px显示）
- 表单验证和提交
- 通知消息提示

### 动画效果
- 淡入淡出 (fade-up, fade-left, fade-right)
- 滚动触发动画
- 悬停效果

## 联系方式

**宁波阿密格供应链有限公司**

- 📞 电话：0574-87059858 / 18649665263
- 📧 邮箱：jonson@amigos-supply.com
- 📍 地址：宁波市鄞州区姚隘路796号东城国际1111室
- 🌐 网站：[amigos-supply.com](http://amigos-supply.com)

## 浏览器支持

- Chrome (最新版)
- Firefox (最新版)
- Safari (最新版)
- Edge (最新版)
- 移动端浏览器

## 开发计划

- [ ] 添加更多语言支持
- [ ] 集成在线客服系统
- [ ] 添加物流追踪功能
- [ ] 优化 SEO 和性能
- [ ] 添加后台管理系统

## License

Copyright © 2018-2026 宁波阿密格供应链有限公司. All rights reserved.

## 维护者

[@chaihuasong](https://github.com/chaihuasong)
