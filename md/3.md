# 主流Web框架在Cloudflare Workers的部署指南
![](../assets/others/3.jpg)


## 开发环境必需：
### 【[视频教程](https://www.bilibili.com/video/BV1sFSqYGEem/)】

### 1. node、npm、pnpm

#### Node.js 安装
- Node.js 安装方法: 查看[官方文档](https://nodejs.org/en/download/)
- 建议安装 LTS (长期支持版本)
- 安装完成后，验证安装:
```bash
node -v
npm -v
```

#### pnpm 安装与配置
pnpm 安装方法: 查看[官方文档](https://pnpm.io/installation)
```bash
npm install -g pnpm
```

验证 pnpm 安装:
```bash
pnpm -v
```

配置 pnpm:

1. 设置镜像源为国内镜像源（推荐使用腾讯源或阿里源）
```bash
# 腾讯源
pnpm config set registry https://mirrors.cloud.tencent.com/npm/

# 或使用阿里源
pnpm config set registry https://registry.npmmirror.com/
```

2. 验证镜像源设置
```bash
pnpm config get registry
```

### 2. Cloudflare Workers 开发环境

#### 准备工作
1. 注册 Cloudflare 账号：访问 [Cloudflare官网](https://dash.cloudflare.com/sign-up) 注册
2. 开通 Workers 服务：在 Cloudflare 控制台中开通 Workers & Pages 服务

#### 支持的框架类型
Cloudflare Workers 支持部署多种主流前端框架：

1. **全栈框架**
- Remix (推荐)
- Next.js (推荐,等next15版本)
- Nuxt
- SvelteKit
- Qwik City

2. **静态站点框架**
- Astro
- Docusaurus
- Gatsby
- Vue
- Angular
- React
- Solid

#### 创建项目示例

1. **Remix 项目**
```bash
pnpm create cloudflare@latest my-remix-app --framework=remix --experimental
```

2. **Next.js 项目**
```bash
下期更新
```

#### 项目开发与部署流程

1. **进入项目目录**
```bash
cd my-remix-app
```

2. **安装依赖**
```bash
上面的一键命令已经安装，这个可选
pnpm install
```

3. **本地开发**
```bash
pnpm run dev
```
- 默认访问地址：http://localhost:5173
- 支持热更新
- 支持本地调试 Workers 功能

4. **部署到 Cloudflare Workers**
```bash
pnpm run deploy
```

部署成功后，你会获得一个 `*.workers.dev` 的workers域名, 访问地址为：https://your-app-name.workers.dev

#### 自定义域名配置

1. 在 Cloudflare 控制台中添加你的域名
2. 在 Workers 设置中绑定自定义域名

### 3. 常见问题解决

1. **部署失败问题**
- 检查 `wrangler.toml` 配置是否正确
- 确认账号是否有足够的配额
- 查看 `wrangler deploy` 命令的错误日志

2. **性能优化建议**
- 使用 Cloudflare 的 KV 存储或 D1 数据库
- 合理设置缓存策略
- 使用 Cloudflare Images 优化图片加载

3. **开发过程问题**
- 如遇权限问题，使用管理员权限运行命令
- 本地开发端口冲突，可在 `wrangler.toml` 中修改端口配置
- 确保 `node` 版本符合项目要求

4. **框架特定问题**
- Remix：注意路由配置和数据加载策略
- Next.js：部分高级特性可能需要调整以适应 Workers 环境
- Vue/React：确保构建输出适配 Workers 运行环境

更多参考资料：
- [Cloudflare Workers 官方文档](https://developers.cloudflare.com/workers/)
- [Workers 框架部署指南](https://developers.cloudflare.com/workers/frameworks/)
- [Workers 限制与配额说明](https://developers.cloudflare.com/workers/platform/limits/)