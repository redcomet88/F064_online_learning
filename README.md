# F064 vue+flask知识图谱在线学习系统

> 完整项目收费，可联系QQ: 81040295 微信: mmdsj186011 注明从github来的，谢谢！
也可以关注我的B站： 麦麦大数据 https://space.bilibili.com/1583208775
> 
> 
> 关注B站，私信获取！   [麦麦大数据](https://space.bilibili.com/1583208775)
编号:  F064

## 视频

[video(video-F2pTowJj-1767055014363)(type-csdn)(url-https://live.csdn.net/v/embed/507926)(image-https://i-blog.csdnimg.cn/direct/3dc7e3ecb9f942eba5ccb884b4ec3736.png)(title-F064-基于知识学习系统python-水印)]

## 1 系统简介
系统简介：本系统是一个基于Vue+Flask+MySQL+Neo4j构建的**基于Mooper数据集的学习系统**。其核心功能围绕**课程知识图谱的构建与可视化、课程与习题的在线学习、以及学习数据的分析**。主要功能模块包括：用户端的课程学习、习题练习、知识图谱可视化、个人中心，以及管理员端的数据大屏分析与数据查询。
## 2 功能设计
该系统采用前后端分离的B/S架构模式，基于Vue+Flask+MySQL+Neo4j技术栈实现。前端通过Vue.js框架搭建响应式界面，结合Vuetify组件库提供友好的用户交互体验，使用Vue-Router进行页面路由管理，Axios实现与后端的异步数据交互。Flask后端负责构建RESTful API服务，通过SQLAlchemy操作MySQL数据库存储用户信息、课程信息等结构化数据，Py2neo作为Neo4j的驱动库，用于在图数据库中构建、查询和管理知识图谱。在**知识图谱构建**功能方面，系统利用Python对Mooper数据集进行处理，抽取特定学科（如“操作系统”）的子集（包含课程、练习、习题），并构建出其节点与关系，最终存入Neo4j，形成结构化的知识网络，支撑前端的可视化展示和智能查询。

### 2.1系统架构图
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/9062032c1bb640b48dd793a1a89f8408.jpeg)
系统架构分为前端、后端和数据层。用户通过浏览器访问前端（Vue）界面，前端通过HTTP请求与Flask后端进行通信。Flask后端负责处理业务逻辑，并与MySQL和Neo4j进行数据交互。MySQL用于存储常规的结构化数据，如用户信息、课程元数据等；Neo4j则作为图数据库，用于存储和查询由学习知识图谱构建的节点与关系。系统通过py2neo库连接Neo4j，实现知识图谱的增删改查。
### 2.2 功能模块图
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/a7757262e2d54629a32c90852c4e9024.jpeg)
主要功能模块有：
1.  **用户端模块**：
    *   课程搜索
    *   学习课程
    *   习题学习
    *   知识图谱可视化
    *   数据大屏（部分用户可见）
    *   个人设置
    *   登录 & 注册
2.  **管理员端模块**：
    *   数据查询
    *   知识图谱构建
    *   数据大屏
    *   课程管理
    *   用户管理

### 3.1 登录 & 注册
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/9a0bcd44a2cb477a8f2fabcf50d88be7.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/e5d7e56b52d24088a6041e1c29b1c025.png)
系统提供标准的登录与注册功能。用户可以通过输入用户名和密码进行登录，或通过注册获取新账户。登录时会验证凭证，并生成会话。注册时会检查用户名的唯一性，并将新用户信息加密后存储到MySQL数据库中。
### 3.2 知识图谱可视化
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/d73a66e720064d30a806211d612d884b.png)
系统通过D3.js在前端实现知识图谱的动态可视化。课程相关知识图谱（节点包括：sub_discipline, course, exercise, challenge）存储在Neo4j数据库中。用户可以在图谱中进行关键词模糊检索，点击节点可查看其详细信息，支持缩放、拖拽等交互操作。
### 3.3 课程搜索

课程以卡片形式在首页展示，点击卡片可进入课程详情页面。详情页展示课程名称、简介、所属学科、评分等信息，并提供“学习课程”按钮，用户点击后可将该课程添加到自己的“我的课程”列表。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/241cdfbd71894f8086ce93038aea2e96.png)
### 3.4 学习课程
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/28a584b6e2544e0cb74e80c09d3b2460.png)
“学习课程”功能是课程的收藏与学习入口。用户点击“学习课程”后，系统会将该课程的ID与用户ID关联存储到数据库中，实现类似收藏的功能，方便用户后续查找和复习。

### 3.5 习题的学习
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/9a5c43d25b6c43f2ad20ceae6a87340a.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/c6ccda72fd0c44ec92aa40c1b5333873.png)

当用户加入学习课程后，在课程详情页下会展示该课程包含的所有练习题集（exercise）。用户可以逐个点击进入，查看其下包含的每一道习题（challenge）的具体题干和答案。当用户点击“已学习”按钮时，系统会更新该习题的学习状态和用户的学习进度。
**加入了AI学习伴侣功能，用户可以进行随时的提问，通过接入了deepseek的深度思考功能。**
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/17b61cb2871b4fbc9d9b75020a22b8a0.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/bb8fac1fb57d410c9ea9cc48ed197634.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/5aa12771629c4daf9cb5b45552b2ad15.png)
deepseek接入：
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/89cefb818a5e49019cad316e7f62646b.jpeg)
没有打开深度思考：
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/5eb03b557eb6430588fcab87d18fea73.png)
### 3.6 数据大屏
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/646fb915ba0249febbd6670d21062abf.png)
系统提供一个数据大屏，通过ECharts库展示系统内的各种分析数据。它包含了丰富的可视化图表，如柱状图、饼图、环图、可拖动的折线图（x轴）以及滚动的柱状图，用于直观地展示课程活跃度、用户分布、学习进度等信息。
### 3.7 数据查询
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/4efd1239791f4b01bfe8a9fddee7af6b.png)
管理员可以进入数据查询模块，通过表格形式浏览和筛选系统内的课程信息，如课程名称、所属学科、创建时间等，支持按条件查询和导出。
### 3.8 个人设置
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/09e451b7c11e4430aec9fea3d7ee5363.png)
个人设置页面允许用户修改个人信息和头像。用户可以上传本地图片作为头像，系统将图片保存到指定文件夹，并在数据库中更新用户头像路径。用户也可以修改其他基本信息。
### 3.9 知识图谱构建
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/6d4d7085fd3c40ad850d6caa140f9d8a.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/031552447c814766bd3d73aa2fc826a6.png)
该功能由管理员在后台执行。系统首先将Mooper数据集中的数据子集（如`sub_discipline`为“操作系统”的数据）导入MySQL。然后，通过Python脚本，使用Py2neo连接Neo4j，遍历MySQL中的数据，根据其定义（`sub_discipline` -> `course` -> `exercise` -> `challenge`）构建出相应的节点和关系，最终形成一个完整的知识图谱。这个过程实现了从原始数据到结构化知识的转化。

### 3.10 用户管理
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/c683cefe96f84c4f907ef09bf3018164.png)
管理员可以查看所有用户的信息（包括用户名、注册时间、角色等），并支持对用户进行删除等操作。
### 3.11 权限管理
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/050ddd98edcf4aff8d6f2b9cea7c9e30.png)
系统采用基于角色的访问控制。管理员可以创建不同角色（如普通用户、管理员），并为每个角色分配相应的功能权限，例如是否可以访问数据大屏、是否可以进行知识图谱构建等，以保障系统的安全性和管理的便捷性。
## 4程序核心算法代码
### 4.1 代码说明
代码介绍：
1.  **知识图谱构建**：使用Py2neo库连接Neo4j，根据从MySQL中抽取的课程、习题数据，构建出`sub_discipline`、`course`、`exercise`、`challenge`四个实体类型，并创建它们之间的`HAS_COURSE`、`HAS_EXERCISE`、`HAS_CHALLENGE`等关系，形成学习知识图谱。
2.  **图灵搜索**：在前端，利用D3.js的力导向图算法渲染Neo4j中的知识图谱数据，支持用户对节点进行缩放、拖拽和交互式查询。
### 4.2 流程图
```mermaid
graph TD
    A[从Mooper数据集抽取"操作系统"相关数据] --> B[导入MySQL数据库]
    B --> C[启动知识图谱构建程序]
    C --> D[通过Py2neo连接Neo4j]
    D --> E[从MySQL读取数据]
    E --> F[创建节点与关系]
    F --> G[写入Neo4j图数据库]
    G --> H[完成知识图谱构建]
```
### 4.3 代码实例
```python
# 1. 使用Py2neo构建知识图谱关系
from py2neo import Graph, Node, Relationship

# 连接Neo4j
graph = Graph("bolt://localhost:7687", auth=("neo4j", "password"))

# 创建节点和关系
sub_discipline = Node("SubDiscipline", name="操作系统")
course = Node("Course", name="计算机操作系统", description="课程描述...")
exercise = Node("Exercise", name="进程管理练习题", description="...")
challenge = Node("Challenge", id="1001", question="进程调度的必要性是什么？", answer="答案...")

# 创建关系
r1 = Relationship(sub_discipline, "HAS_COURSE", course)
r2 = Relationship(course, "HAS_EXERCISE", exercise)
r3 = Relationship(exercise, "HAS_CHALLENGE", challenge)

# 将整个图谱提交
graph.create(sub_discipline, course, exercise, challenge, r1, r2, r3)
```

```sql
-- 2. Neo4j查询知识图谱的Cypher语句
MATCH (s:SubDiscipline {name: "操作系统"})-[:HAS_COURSE]->(c:Course)-[:HAS_EXERCISE]->(e:Exercise)-[:HAS_CHALLENGE]->(ch:Challenge)
RETURN s, c, e, ch
```

---
> 关注B站，私信获取！   [麦麦大数据](https://space.bilibili.com/1583208775)
> 
> 文章结尾部分有CSDN官方提供的学长 联系方式名片
> 
> 文章结尾部分有CSDN官方提供的学长 联系方式名片
