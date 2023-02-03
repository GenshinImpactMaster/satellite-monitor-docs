# API文档
## 业务侧
业务侧的API统一由SpringBoot应用提供, 路径为`BASE_URL/<TITLE_PATH>`

业务侧HTTP请求方法统一为POST, 格式统一为`application/x-www-form-urlencoded`

鉴权方法统一采用JWT(Token保存在`header.Authorization`中)， 需要鉴权的会使用 :material-account-key: `<用户组>`标注, 若无标注则默认需要User权限, `<用户组>`为`NULL`则表示不需要任何权限

### 通用泛型
下面使用typescript语法来标注此业务相关的通用类型
```typescript
// 带有分页的请求
interface Pageable {
  pageNumber: number;
  pageSize: number;
}
// 分页组件返回的类型
interface Page<T> {
  content: T[];
  totalElements: number;
  totalPages: number;
  last: boolean;
  size: number;
  number: number;
  numberOfElements: number;
}
// 用户
interface User {
  uuid: string;
  name: string;
  role: string;
}

interface UserPermission {
  user: User;
  instanceIds: string[];
}

interface ResourceType {
  /** 资源类型的key */
  name: string;
  /** 资源类型的中文名 */
  nameCN: string;
  /** 资源类型的相关描述 */
  description: string;
  /** 资源类型的metrics */
  metrics: string[];
  /** showMeta */
  showMeta: string[];
}

interface Instance {
  id: string;
  meta: Record<string, string>;
  name: string;
  description: string;
  type: string;
  createaAt: number;
  status: number;
}

interface InstanceDetails extends Omit<Instance, 'type'> {
  type: ResourceType;
}

interface Metric {
  name: string;
  nameCN: string;
  description: string;
  statistics: string[];
}

```

### 用户模块
#### Login
:material-account-key: NULL

| 参数       | 类型    |  描述 |
| ---------- | ------- | ---- |
| `id`       | `string`  | 用户的`UUID`|
| `password` | `string` | 用户密码   |

| 返回       | 类型     |  描述 |
| ---------- | ------- | ---- |
| `user`     | `User`  | 包含用户基本信息 |
| `token`    | `string`  | 用户密码   |

#### FindUserById
:material-account-key: ADMIN

| 参数       | 类型    |  描述 |
| ---------- | ------- | ---- |
| `userId`       | `string`  | 用户的`UUID`|


| 返回       | 类型     |  描述 |
| ---------- | ------- | ---- |
| `...User`     | `...User`  | 包含用户基本信息(展开) |

#### FindUserByName
:material-account-key: ADMIN

| 参数       | 类型    |  描述 |
| ---------- | ------- | ---- |
| `name`     | `string`  | 用户的`UUID`|
| `...Pageable`     | `...Pageable`  | 分页参数 |

| 返回       | 类型     |  描述 |
| ---------- | ------- | ---- |
| `...Page<User>`     | `...Page<User>`  | 带分页的包含用户的基本信息(展开) |

#### ListUser
:material-account-key: ADMIN

| 参数       | 类型    |  描述 |
| ---------- | ------- | ---- |
| `query`       | `Object`  | 符合MongoDB Query的JSON表达式 |
| `...Pageable`     | `...Pageable`  | 用户的`UUID`|

| 返回       | 类型     |  描述 |
| ---------- | ------- | ---- |
| `...Page<User>`     | `...Page<User>`  | - |

#### AddUser
:material-account-key: ADMIN

!!! note "NEED P"

| 参数       | 类型    |  描述 |
| ---------- | ------- | ---- |
| `name`         | `string`  | 用户名 |
| `password`     | `string`  | 用户密码 |
| `permission`   | `'ADMIN' | 'USER'`  | 用户权限 |

| 返回       | 类型     |  描述 |
| ---------- | ------- | ---- |
| `...User`     | `...User`  | 用户的基本信息 |

#### UpdateUser
:material-account-key: ADMIN

!!! note "NEED P"

| 参数       | 类型    |  描述 |
| ---------- | ------- | ---- |
| `id`         | `string`  | 用户`UUID` |
| `name`         | `string`  | 用户名 |
| `password`     | `string`  | 用户密码 |
| `permission`   | `'ADMIN' | 'USER'`  | 用户权限 |

| 返回       | 类型     |  描述 |
| ---------- | ------- | ---- |
| `...User`     | `...User`  | 用户的基本信息 |

#### RefreshToken
刷新Token

| 返回       | 类型     |  描述 |
| ---------- | ------- | ---- |
| `user`     | `User`  | 用户的基本信息 |
| `token`     | `string`  | 新的token |

#### ListUserPermission
:material-account-key: ADMIN

| 参数       | 类型    |  描述 |
| ---------- | ------- | ---- |
| `query`       | `Object`  | 符合MongoDB Query的JSON表达式 |
| `...Pageable`     | `...Pageable`  | - |

| 返回       | 类型     |  描述 |
| ---------- | ------- | ---- |
| `...Page<UserPermission>`     | `...Page<UserPermission>`  | 相关用户权限的列表 |

### 资源模块
#### ListResourceType

| 参数       | 类型    |  描述 |
| ---------- | ------- | ---- |
| `...Pageable`     | `...Pageable`  | - |

| 返回       | 类型     |  描述 |
| ---------- | ------- | ---- |
| `...Page<ResourceType>`     | `...Page<ResourceType>`  | - |

#### ListAllResourceType

| 返回       | 类型     |  描述 |
| ---------- | ------- | ---- |
| `...ResourceType[]`     | `...ResourceType[]`  | 全量的资源类型 |

#### ListInstance

| 参数       | 类型    |  描述 |
| ---------- | ------- | ---- |
| `query`       | `Object`  | 符合MongoDB Query的JSON表达式 |
| `...Pageable`     | `...Pageable`  | - |

| 返回       | 类型     |  描述 |
| ---------- | ------- | ---- |
| `...Page<Instance>`     | `...Page<Instance>`  | - |


#### GetInstanceInfo
!!! note "NEED P"

| 参数       | 类型    |  描述 |
| ---------- | ------- | ---- |
| `id`       | `string`  | instance的id |

| 返回       | 类型     |  描述 |
| ---------- | ------- | ---- |
| `...InstanceDetails`     | `...InstanceDetails`  | - |

#### GetResourceType
!!! note "NEED P"

| 参数       | 类型    |  描述 |
| ---------- | ------- | ---- |
| `type`       | `string`  | 通过`resourceType.type`查找对应的`resourceType` |

| 返回       | 类型     |  描述 |
| ---------- | ------- | ---- |
| `...ResourceType`     | `...ResourceType`  | - |

### 度量单位模块
#### ListAllMetrics

| 返回       | 类型     |  描述 |
| ---------- | ------- | ---- |
| `...Metric[]`     | `...Metric[]`  | - |

#### ListMetrics

| 参数       | 类型    |  描述 |
| ---------- | ------- | ---- |
| `query`       | `Object`  | 符合MongoDB Query的JSON表达式 |
| `...Pageable`     | `...Pageable`  | - |

| 返回       | 类型     |  描述 |
| ---------- | ------- | ---- |
| `...Page<Metric>`     | `...Page<Metric>`  | - |

#### UpdateMetric
:material-account-key: ADMIN

| 参数       | 类型    |  描述 |
| ---------- | ------- | ---- |
| `name`       | `string`  | Metric.name |
| `nameCN`     | `string`  | Metric.nameCN |
| `description`     | `string`  | Metric.description |

| 返回       | 类型     |  描述 |
| ---------- | ------- | ---- |
| `...Metric`     | `...Metric`  | - |

## 监控侧
### 查询时序数据
#### QueryMetric


| 参数       | 类型    |  描述 |
| ---------- | ------- | ---- |
| `name`       | `string`  | Metric.name |
| `nameCN`     | `string`  | Metric.nameCN |
| `description`     | `string`  | Metric.description |

| 返回       | 类型     |  描述 |
| ---------- | ------- | ---- |
| `...Metric`     | `...Metric`  | - |