# Mermaid使用

```mermaid
graph LR
A[开始] --> B(流程)
B --> C{判断}
C -->|结果1| D[结束]
C -->|结果2| E[结束]
```

## 简单流程图

```mermaid
graph LR
  A[开始] --> B[流程1]
  B --> C[流程2]
  C --> D[结束]
```

```mermaid
graph TD
    A[开始]-->B(步骤1)
    B---->C(步骤2)
    B--描述文本-->D(步骤3)
    C==>E(步骤4)
    D==>E
    E--选项1-->F(步骤5)
    E-.选项2.->G(步骤6)
    G==>H(步骤7)
    G-.选项3.->I(步骤8)
    I-.确定.->H
    
    subgraph 一组节点
        B
        C
        D
    end
```

```mermaid
graph TD
    A[开始] -->|初始化| B(设置参数)
    B --> C{条件}
    C -->|是| D[步骤1]
    C -->|否| E[步骤2]
    B --> F(调整参数)
    E --> F
    D --> G((输出结果))
    F --> G
    G -->|完成| H[结束]
```

## 复杂流程图

```mermaid
graph LR
  A[开始]-->B[流程1]
  B-->C[判断条件]
  C-->|条件成立|D[流程2]
  D-->E[判断条件]
  E--> |条件成立| F[流程3]
  F-->|否则|G[流程4]
  E-->|条件不成立|G[流程4]
  G-->H[结束]
```

## 子图

```mermaid
flowchart LR
  subgraph A
  物品-->B[计算1]
  B-->C(判断1)
  C-->|条件1| D[输出结果1]
  C-->|条件2| E[计算2]
  E-->D
  end

  subgraph B
  客户-->F[计算3]
  F-->G(判断2)
  G-->|条件3|H[输出结果2]
  G-->|条件4|I[计算4]
  I-->H
  end

  A-->B
  F-->C
```

## 类图

```mermaid
classDiagram
  class Animal {
    +name: String
    +eat()
  }
```

## 状态图

```mermaid
stateDiagram-v2
  [*] --> Off
  Off --> Starting : Power on
  Starting --> On : Start success
  On --> Off : Power off
  On --> Suspended : Sleep
  Suspended --> Off : Power off
  On --> Starting : Restart
```

## 时序图

```mermaid
sequenceDiagram
  participant A
  participant B
  A ->> B : 请求数据
  B -->> A : 返回数据
```

## 甘特图

```mermaid
gantt
  title 项目计划
  dateFormat  YYYY-MM-DD
  section 研发
  设计 :a1, 2018-01-01, 30d
  开发 :a2, 2018-01-03, 60d
  测试 :a3, after a2, 20d
  section 上线
  发布 :b1, after a3, 2d
  测试 :b2, after b1, 5d
```

## 树状图

```mermaid
graph TD
  A[开始] --> B[分类1]
  B --> C[子分类1]
  B --> D[子分类2]
  C --> E[项目1]
  C --> F[项目2]
  D --> G[项目3]
  D --> H[项目4]
```

## 矩形图

```mermaid
graph TD
  subgraph 系统
    A(用户) -- 输入 --> B(系统)
    B -- 处理 --> C{结果正确?}
    C -- 是 --> D(输出结果)
    C -- 否 --> E(返回错误信息)
  end
```

## 异步流程图

```mermaid
sequenceDiagram
  A->>B: 请求A
  B->>C: 请求B
  B->>D: 请求C
  C-->>B: 返回C
  D-->>B: 返回D
  B-->>A: 返回B
```

## 流程图

```mermaid
flowchart TD
  A[开始] -->|条件1| B[流程1]
  B -->|条件2| C[流程2]
  C -->|条件3| D[流程3]
  D -->|条件4| E[结束]
```

## 状态转换图

```mermaid
stateDiagram
  [*] --> 状态1
  状态1 --> 状态2 : 事件1
  状态1 --> 状态3 : 事件2
  状态2 --> 状态3 : 事件3
  状态3 --> 状态1 : 事件4
  state 状态1 {
    [*] --> 子状态1
    子状态1 --> 子状态2 : 子事件1
    subgraph 子状态组
      子状态2 --> 子状态3 : 子事件2
    end
    子状态3 --> 子状态1 : 子事件3
  }
```

## 强调样式

```mermaid
graph TD
  A[开始] -->|条件1| B[流程1]
  B -->|条件2| C[流程2]
  C -->|条件3| D[流程3]
  D -->|条件4| E[结束]
  style A fill:#BEE7E9,stroke:#333,stroke-width:4px
  style B fill:#BEE7E9,stroke:#333,stroke-width:4px
  style D fill:#BEE7E9,stroke:#333,stroke-width:4px
```

## 字体样式

```mermaid
graph TD
  A[开始] -->|条件1| B[流程1]
  B -->|条件2| C[流程2]
  C -->|条件3| D[流程3]
  D -->|条件4| E[结束]
  style A font-size:14px,fill:#BEE7E9,stroke:#333,stroke-width:4px
  style B font-size:14px,fill:#BEE7E9,stroke:#333,stroke-width:4px
```

## 样式继承

```mermaid
graph TD
  A[开始] -->|条件1| B[流程1]
  B -->|条件2| C[流程2]
  C -->|条件3| D[流程3]
  D -->|条件4| E[结束]
  style B extends A,fill:#BEE7E9,stroke:#333,stroke-width:4px
  style C extends B,fill:#E5D7D7
  style D extends B,fill:#E5D7D7
```

## 自定义节点类型

```mermaid
classDiagram
  class MyNode{
    -name : String
    -level : Integer
    +getName() : String
  }
```

## 点击事件

```mermaid
graph TD
  A[开始] -->|条件1| B[流程1]
  B -->|条件2| C[流程2]
  click C "alert('This is C node')" "点击C节点"
  C -->|条件3| D[流程3]
  D -->|条件4| E[结束]
```

## 容器

```mermaid
graph TB
  subgraph A
  	B
  end
```

## Git图

```mermaid
gantt
  title Git 进化史
  dateFormat YYYY-MM-DD
  section 远古时代
  创建 Git :a1, 2005-04-12, 15d
  section 现代化时代
  GitHub 购买 Git :a2, 2018-06-04, 1d
  section 近期时 
  Microsoft 收购 GitHub :a3, 2018-06-04, 1d
```

## 用户定义样式

```mermaid
flowchart TD
  A[项目] -->|使用存储过程| B((数据库))
  B -->|更新数据表| C{数据表}
  C -->|检查结果| D[是否满足要求]
  style A fill:#BEE7E9,stroke:#333,stroke-width:4px
  style B fill:#BEE7E9,stroke:#333,stroke-width:4px,stroke-dasharray: 5, 5
  style C fill:#BEE7E9,stroke:#333,stroke-width:4px,stroke-dasharray: 5, 5
  style D fill:#BEE7E9,stroke:#333,stroke-width:4px,stroke-dasharray: 5, 5,font-size:14px
```

## 数字属性

```mermaid
graph TD
  A[顶部] ==>|50| B[中部]
  B <==>|25| C[底部]
```

## 饼图

```mermaid
pie title 人员构成
  "工程师" : 43
  "销售" : 20
  "市场" : 17
  "其他" : 5
  "管理" : 15
```



