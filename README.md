# GECS

> **适用于 Godot 4.x 的实体组件系统（Entity Component System）**

通过清晰分离数据与逻辑，构建可扩展、易维护的游戏。GECS 无缝集成 Godot 的节点系统，同时提供强大的基于查询的实体筛选功能。

## ✨ 核心特性

- 🎯 **Godot 集成** — 与节点、场景和编辑器协同工作
- 🚀 **高性能** — 优化的查询机制，支持自动缓存
- 🔧 **灵活查询** — 通过组件、关系或属性查找实体
- 🔍 **调试查看器** — 实时检查与性能监控
- 📦 **编辑器支持** — 可视化组件编辑与场景集成
- 🎮 **实战验证** — 已用于多款正在积极开发的游戏


```gdscript
# 使用组件创建实体
var player1 = Entity.new()
player1.add_component(C_Health.new(100))
player1.add_component(C_Velocity.new(Vector2(5, 0)))

var player2 = Entity.new()
player2.add_component(C_Health.new(100))
player2.add_component(C_Velocity.new(Vector2(-5, 0)))

# 将实体添加到世界
ECS.world.add_entities([player1, player2])

# 为实体添加关系
# Player 1 是 Player 2 的盟友
player1.add_relationship(Relationship.new(C_AllyTo.new(), player2))
# Player 2 对 Player 1 有点怀疑
player2.add_relationship(Relationship.new(C_SuspiciousOf.new(), player1))

# 组件仅定义数据
class_name C_Velocity extends Component

@export var velocity := Vector3.ZERO


# 系统处理具有特定组件的实体
class_name VelocitySystem extends System

# 系统通过查询选择实体并迭代其组件
func query() -> QueryBuilder:
    return q.with_all([C_Velocity, C_Transform]).iterate([C_Velocity, C_Transform])

# 系统实现 process 方法来处理选中的实体
func process(entities: Array[Entity], components: Array, delta: float) -> void:
    var c_velocities = components[0] # C_Velocity（iterate 中第一个）
    var c_transforms = components[1] # C_Transform（iterate 中第二个）

    # 处理所有匹配查询的实体上的速度与变换组件
    for i in entities.size():
        var c_velocity := c_velocities[i] as C_Velocity
        var c_transform := c_transforms[i] as C_Transform
        c_transform.transform.global_position += c_velocity.velocity * delta

# 将系统添加到世界
ECS.world.add_system(VelocitySystem.new())

# 推进世界并调用所有系统
ECS.world.process(delta)
```

⚡ 快速开始
安装：下载到 addons/gecs/ 目录，并在项目设置中启用插件
阅读指南：5 分钟内运行你的第一个 ECS 项目 →
深入学习：理解核心 ECS 概念 →
📚 完整文档
所有文档均位于插件文件夹中：

→ 完整文档索引

快速导航
入门指南 — 构建你的第一个 ECS 项目（5 分钟）
核心概念 — 理解实体、组件、系统与关系（20 分钟）
最佳实践 — 编写可维护的 ECS 代码（15 分钟）
故障排除 — 快速解决常见问题
高级功能
组件查询 — 高级基于属性的过滤
关系系统 — 实体链接与关联
观察者 — 响应组件变化的响应式系统
性能优化 — 让你的游戏运行更快
🎮 示例游戏
GECS-101 — 一个简单示例
Zombies Ate My Neighbors — 动作街机游戏
打砖块克隆版 — 经典打砖块游戏
🌟 社区
Discord：加入我们的社区
问题反馈：报告 bug 或请求新功能
讨论区：提问并分享你的项目
📄 许可证
MIT — 详情请参阅 LICENSE 。

GECS 按“现状”提供。如果它坏了，你得自己承担后果。 😄

Star History Chart
