# 中年人招聘系统

基于uni-app + uniCloud的中年人招聘系统，专注于为中年求职者提供更好的就业机会。

## 项目简介

本项目是一个专门面向中年人群的招聘平台，采用uni-app + uniCloud技术栈开发，支持多端运行（H5、微信小程序、App）。系统分为求职者端和企业端两个角色，实现了职位发布、职位浏览、职位申请、消息通知等核心功能。

## 技术栈

- 前端框架：uni-app（Vue3）
- 后端服务：uniCloud
- 数据库：uniCloud云数据库
- 云函数：基于Node.js的uniCloud云函数
- UI设计：自定义设计，未使用第三方UI库
- 开发工具：HBuilderX

## 功能模块

### 1. 用户模块
- 用户注册（求职者/企业）
- 用户登录
- 个人信息管理
- 企业信息管理

### 2. 职位模块
- 职位发布（企业）
- 职位列表浏览
- 职位搜索
- 职位详情查看
- 职位收藏
- 职位申请

### 3. 简历模块
- 求职者简历管理
- 工作经验管理
- 技能特长展示
- 教育背景管理

### 4. 应聘模块
- 简历投递
- 应聘记录查看
- 企业处理应聘
- 面试邀请

### 5. 消息模块
- 系统消息
- 应聘通知
- 面试邀请
- 企业消息
- 消息已读状态管理

## 项目结构

```
├─pages                    // 页面文件夹
│  ├─index                // 首页
│  ├─login                // 登录页
│  ├─register             // 注册页
│  ├─job                  // 职位相关页面
│  ├─profile              // 个人中心
│  ├─message              // 消息中心
│  ├─application          // 应聘管理
│  └─collection           // 收藏管理
├─components              // 组件文件夹
│  └─loading             // 加载组件
├─static                  // 静态资源
│  └─images              // 图片资源
└─uniCloud-aliyun        // 云开发目录
   ├─cloudfunctions      // 云函数
   │  ├─userInformationCenter    // 用户中心
   │  ├─jobCenter               // 职位中心
   │  └─messageCenter           // 消息中心
   └─database            // 数据库集合
      ├─userInformations.schema.json    // 用户表
      ├─jobs.schema.json               // 职位表
      ├─applications.schema.json       // 应聘表
      └─messages.schema.json           // 消息表
```

## 环境搭建

### 开发环境要求
- HBuilderX 3.0+
- Node.js 12.0+
- 微信开发者工具（可选，用于小程序开发）

### 安装步骤

1. 克隆项目
```bash
git clone [项目地址]
```

2. 使用HBuilderX打开项目

3. 云服务空间初始化
- 打开uniCloud目录
- 创建新的云服务空间（阿里云）
- 关联云服务空间
- 上传所有云函数
- 初始化数据库集合

4. 运行项目
- 选择运行到内置浏览器（H5）
- 运行到微信开发者工具（小程序）
- 运行到手机或模拟器（App）

## 部署说明

### H5部署
1. 在HBuilderX中选择"发行"→"网站-H5手机版"
2. 将生成的dist/build/h5文件夹部署到web服务器

### 微信小程序部署
1. 在HBuilderX中选择"发行"→"小程序-微信"
2. 将生成的dist/build/mp-weixin导入微信开发者工具
3. 在微信开发者工具中上传发布

### App发布
1. 在HBuilderX中选择"发行"→"原生App-云打包"
2. 配置应用标识、图标等信息
3. 选择证书文件
4. 等待云打包完成后下载安装包

## 注意事项

1. 数据安全
- 请及时修改云函数的安全规则
- 定期备份数据库
- 注意保护用户敏感信息

2. 性能优化
- 合理使用云函数
- 避免频繁的数据库操作
- 图片资源建议使用CDN加速

3. 开发建议
- 遵循Vue3的组件开发规范
- 使用rpx单位适配多端
- 保持良好的代码注释习惯

## 数据库设计

本系统使用uniCloud云数据库，采用NoSQL文档型数据库结构。系统包含5个主要数据集合，分别存储用户信息、职位信息、应聘申请、消息通知和职位收藏数据。

### 数据表结构

#### 1. userInformations（用户信息表）

存储系统中所有用户（求职者和企业）的基本信息和详细资料。

| 字段名 | 类型 | 必填 | 描述 |
| ----- | ---- | ---- | ---- |
| _id | String | 自动生成 | 用户ID，系统自动生成 |
| phone | String | 是 | 手机号，格式：1开头的11位数字 |
| password | String | 是 | 密码 |
| userType | Integer | 是 | 用户类型：1-求职者，2-企业 |
| name | String | 是 | 姓名/企业名称 |
| avatar | String | 否 | 头像URL |
| gender | Integer | 否 | 性别：1-男，2-女（仅求职者） |
| age | Integer | 否 | 年龄（仅求职者） |
| education | String | 否 | 学历（仅求职者） |
| workExperience | Array | 否 | 工作经历（仅求职者） |
| skills | Array | 否 | 技能（仅求职者） |
| introduction | String | 否 | 自我介绍（仅求职者） |
| registeredCapital | String | 否 | 注册资金（仅企业） |
| scale | String | 否 | 企业规模（仅企业） |
| companyDescription | String | 否 | 企业介绍（仅企业） |
| companyImages | Array | 否 | 企业图片（仅企业） |
| createTime | Timestamp | 自动生成 | 创建时间 |
| updateTime | Timestamp | 自动生成 | 更新时间 |

**workExperience（工作经历）子结构：**
- company: 公司名称
- position: 职位
- startTime: 开始时间
- endTime: 结束时间
- description: 工作描述

#### 2. jobs（职位信息表）

存储企业发布的职位信息。

| 字段名 | 类型 | 必填 | 描述 |
| ----- | ---- | ---- | ---- |
| _id | String | 自动生成 | 职位ID，系统自动生成 |
| title | String | 是 | 职位名称 |
| salary | String | 是 | 薪资范围 |
| companyId | String | 是 | 企业ID（关联userInformations表） |
| companyName | String | 是 | 企业名称 |
| experience | String | 否 | 工作经验要求 |
| education | String | 否 | 学历要求 |
| location | String | 否 | 工作地点 |
| address | String | 否 | 详细地址 |
| description | String | 是 | 职位描述 |
| requirement | String | 是 | 任职要求 |
| status | Integer | 否 | 状态：1-招聘中，2-已结束 |
| createTime | Timestamp | 自动生成 | 创建时间 |
| updateTime | Timestamp | 自动生成 | 更新时间 |

#### 3. applications（应聘申请表）

记录求职者对职位的申请信息。

| 字段名 | 类型 | 必填 | 描述 |
| ----- | ---- | ---- | ---- |
| _id | String | 自动生成 | 申请ID，系统自动生成 |
| userId | String | 是 | 求职者ID（关联userInformations表） |
| jobId | String | 是 | 职位ID（关联jobs表） |
| status | Integer | 是 | 状态：1-待处理，2-已通过，3-已拒绝 |
| createTime | Timestamp | 自动生成 | 创建时间（申请时间） |
| updateTime | Timestamp | 自动生成 | 更新时间（状态变更时间） |

#### 4. messages（消息表）

存储系统中的消息通知，包括系统消息和应聘通知。

| 字段名 | 类型 | 必填 | 描述 |
| ----- | ---- | ---- | ---- |
| _id | String | 自动生成 | 消息ID，系统自动生成 |
| senderId | String | 是 | 发送者ID（关联userInformations表） |
| receiverId | String | 是 | 接收者ID（关联userInformations表） |
| type | Integer | 是 | 消息类型：1-系统消息，2-应聘通知 |
| title | String | 是 | 消息标题 |
| content | String | 是 | 消息内容 |
| isRead | Boolean | 否 | 是否已读 |
| createTime | Timestamp | 自动生成 | 创建时间（发送时间） |

#### 5. favorites-job（职位收藏表）

记录用户收藏的职位信息。

| 字段名 | 类型 | 必填 | 描述 |
| ----- | ---- | ---- | ---- |
| _id | String | 自动生成 | 收藏ID，系统自动生成 |
| userId | String | 是 | 用户ID（关联userInformations表） |
| jobId | String | 是 | 职位ID（关联jobs表） |
| createTime | Timestamp | 自动生成 | 创建时间（收藏时间） |

### 数据表关系

以下是系统中主要数据表之间的关系：

1. **用户与职位的关系**：
   - 企业用户（userType=2）可以发布多个职位，一个职位只属于一个企业
   - 关联字段：jobs.companyId → userInformations._id

2. **用户与应聘申请的关系**：
   - 求职者用户（userType=1）可以提交多个应聘申请，一个应聘申请只属于一个求职者
   - 关联字段：applications.userId → userInformations._id

3. **职位与应聘申请的关系**：
   - 一个职位可以收到多个应聘申请，一个应聘申请只针对一个职位
   - 关联字段：applications.jobId → jobs._id

4. **用户与消息的关系**：
   - 用户可以发送和接收多条消息
   - 关联字段：messages.senderId/receiverId → userInformations._id

5. **用户与职位收藏的关系**：
   - 用户可以收藏多个职位，一个收藏记录只属于一个用户
   - 关联字段：favorites-job.userId → userInformations._id

6. **职位与职位收藏的关系**：
   - 一个职位可以被多个用户收藏，一个收藏记录只对应一个职位
   - 关联字段：favorites-job.jobId → jobs._id

### 数据访问模式

系统主要通过以下方式访问数据：

1. **用户认证**：通过phone和password字段验证用户身份
2. **职位查询**：根据title、location等字段进行模糊搜索
3. **应聘管理**：
   - 求职者查看自己的应聘记录：applications.userId = 当前用户ID
   - 企业查看收到的应聘：先查jobs获取企业发布的职位，再通过applications.jobId查询
4. **消息通知**：通过receiverId查询用户收到的消息
5. **职位收藏**：通过userId查询用户收藏的职位

### 数据安全

1. **权限控制**：
   - 所有表均开放读取权限
   - 除favorites-job表外，其他表不允许直接删除操作
   - 所有数据修改通过云函数进行权限验证

2. **数据验证**：
   - 手机号格式验证：使用正则表达式确保格式正确
   - 字段长度限制：防止过长文本导致的性能问题
   - 枚举值验证：确保状态字段等只能取预定义的值
