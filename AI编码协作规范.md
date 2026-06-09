# AI 编码协作规范

> 适用场景：单人 / 多人使用 Codex CLI（或 Claude Code）协作开发同一项目。
> 核心原则：**让任何 AI 打开项目就能立刻知道这是干什么的、做到哪了、按什么规范写。**

---

## 1. 项目强制三文档

每个项目根目录必须有以下三份文件：

| 文档 | 给谁读 | 必须包含 |
|------|:--:|------|
| `AGENTS.md` | AI（Codex） | 项目概述、功能清单、架构、技术栈、代码风格 |
| `ROADMAP.md` | AI + 人 | 当前阶段、下一步、阻塞项、已完成里程碑 |
| `README.md` | 人 | 怎么运行、怎么部署、环境依赖 |

### 为什么

- **换人不掉链子**：新接手的人/AI 不用重新"理解项目"。
- **切换 AI 无缝**：从 Codex 换到 Claude Code 或其他工具，三份文档照读不误。
- **自己隔一周回来**：打开 ROADMAP.md 就知道上次停在哪。

---

## 2. AGENTS.md 模板

```markdown
# 项目名称

## 项目概述
一句话说清这个项目是干什么的。

## 功能清单
- 功能 A
- 功能 B

## 技术架构
- **引擎/框架**：Unity 2022 LTS
- **语言**：C#
- **美术管线**：2D 原画（Photoshop） + 3D 建模（Blender）
- **版本控制**：Git

## 目录结构
/Assets/
  Scripts/       ← 游戏逻辑
  Scenes/        ← 场景文件
  Prefabs/       ← 预制体
  Art/           ← 2D + 3D 资源

## 代码规范
- C# 命名：类 PascalCase，方法 PascalCase，变量 camelCase
- 每个 public 方法必须有 XML 注释
- 不写超过 200 行的脚本
- 不用 MonoBehaviour 之外的奇技淫巧
```

---

## 3. ROADMAP.md 模板

```markdown
# 路线图

## 当前阶段
阶段 1：核心玩法原型

## 进行中
- [ ] 玩家移动控制
- [ ] 基础战斗系统

## 下一步
- [ ] 敌人 AI
- [ ] UI 框架搭建

## 阻塞项
- 无

## 已完成
- [x] 项目初始化
- [x] Unity 工程创建
```

---

## 4. README.md 模板

```markdown
# 项目名称

## 运行环境
- Unity 版本：2022.3 LTS
- 目标平台：PC / 移动端

## 快速开始
1. `git clone <repo-url>`
2. Unity Hub → 打开项目
3. 打开 `Scenes/Main.unity` → Play

## 项目结构
见 AGENTS.md
```

---

## 5. Git 工作流

```text
main          ← 稳定发布版
  └── dev     ← 日常开发主线
        ├── feature/xxx   ← 新功能
        ├── bugfix/xxx    ← 修 bug
        └── release/x.x   ← 发布分支
```

**日常流程**：
1. 从 `dev` 拉 `feature/功能名`
2. 开发完成 → 提 PR 到 `dev`
3. Code Review（AI + 人）
4. 合并到 `dev`
5. 积累足够功能 → `release/x.x` → `main`

---

## 6. AI 工具统一配置（多人多工具）

如果团队里有人用 Codex、有人用 Claude Code：

### Codex 用户（`~/.codex/AGENTS.md`）
```markdown
全局和项目配置均以 ~/.claude/CLAUDE.md 为准。
```

### Claude Code 用户（`~/.claude/CLAUDE.md`）
```markdown
# 全局规则
- 始终先读项目的 AGENTS.md 和 ROADMAP.md
- 不要猜测项目信息，读文档
- 修改代码前先看 ROADMAP.md 确认当前优先级
```

**效果**：只维护一份 CLAUDE.md，Codex 通过 AGENTS.md 转发到它。

---

## 7. 单工具简化（仅 Codex）

如果整个团队只用 Codex，不需要 CLAUDE.md → AGENTS.md 转发层：

```text
项目根目录/
  AGENTS.md    ← Codex 直接读这个（项目信息 + 代码规范）
  ROADMAP.md   ← 进度追踪
  README.md    ← 给人看的
```

AGENTS.md 内容照模板写就行，不需要转发语句。

---

> **参考来源**：stormzhang 知识星球 · 2026-06-09
> 
> 最后更新：2026-06-04
