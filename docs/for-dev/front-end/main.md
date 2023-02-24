# 项目结构
项目目录树
```text
main
├── README.md
├── apis # 对接后端apis
│   ├── alert.ts
│   ├── createApi.ts
│   ├── index.ts
│   ├── instance.ts
│   ├── metric.ts
│   ├── resourceType.ts
│   └── user.ts
├── app.vue # 入口文件
├── assets
│   └── style
│       └── main.scss
├── components # 项目中使用到的组件
│   ├── base # 通用组件(与业务没有直接关联)
│   │   ├── BaseTable
│   │   ├── Card
│   │   ├── Chart
│   │   ├── Form
│   │   ├── Layout
│   │   ├── List
│   │   ├── Loading
│   │   ├── Search
│   │   └── Tooltip
│   └── monitor # 业务组件(与业务强关联)
│       ├── Meta
│       ├── alert
│       ├── charts
│       └── list
├── components.d.ts
├── constants
│   ├── metakey.ts
│   ├── metric.ts
│   ├── request.ts
│   └── route.ts
├── dist
├── error.vue
├── interface # TS类型规范
│   ├── alert.ts
│   ├── dashboard.ts
│   ├── instance.ts
│   ├── metric.ts
│   ├── origin.ts
│   ├── request.ts
│   ├── resourceType.ts
│   ├── response.ts
│   ├── strategy.ts
│   ├── user.ts
│   └── userPermission.ts
├── nuxt.config.ts # Nuxt项目配置文件
├── package.json
├── pages # 页面文件
│   ├── dashboard
│   │   ├── index.module.scss
│   │   └── index.tsx
│   ├── index.vue
│   ├── login
│   │   ├── index.module.scss
│   │   └── index.tsx
│   ├── metrics
│   │   └── list.tsx
│   ├── resource
│   │   ├── details
│   │   ├── index.module.scss
│   │   ├── index.tsx
│   │   ├── instance
│   │   └── list
│   ├── strategy
│   │   ├── create
│   │   └── index.tsx
│   └── user
│       ├── list
│       └── permission
├── plugins # Nuxtjs的插件
│   └── antd.client.ts
├── server # BFF层代码, Node Runtime
│   ├── api # BFF层的Api
│   │   └── QueryMetric.post.ts
│   ├── middleware
│   │   └── proxy.ts
│   ├── plugins
│   │   └── error.ts
│   └── utils
│       ├── promRequest.ts
│       ├── promql.ts
│       ├── query.ts
│       └── response.ts
├── store
│   ├── metrics.ts
│   └── user.ts
├── tsconfig.json
├── type.d.ts
└── utils
    ├── config.ts
    ├── copy.ts
    ├── date.ts
    ├── logger.ts
    ├── metric.ts
    ├── permission.ts
    ├── props.ts
    ├── safeRun.ts
    ├── uuid.ts
    └── validate.ts
```

> 该项目是一个`Nuxtjs`的项目, 根据`Nuxt`的规范, 入口文件为`./app.vue`, 在`pages`文件夹的文件会注入到路由中, 无需手动注入.