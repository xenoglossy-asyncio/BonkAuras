# BonkAuras

适用于 **Hordes of Azeroth**（1.12.1 / benilla 客户端）的 WeakAuras 风格 Buff 监控插件。

BonkAuras 把玩家身上的真实 Buff 和 Hordes of Azeroth 的天赋状态放在紧凑、可拖动的图标上。它是一个独立插件：不需要额外库、不修改启动器、不修改服务端。

[English](README.md)

## 功能

- 监控玩家真实 Buff，以及 Hordes of Azeroth 的护盾、冲刺、决心、死疽、受创状态。
- Hordes of Azeroth 状态的名称和描述直接读取 HOA 的本地化，HOA 是什么语言就显示什么语言。
- 层数居中显示在图标内，数值显示在图标上方，剩余时间显示在图标下方。
- 未生效的监控保留在原位：默认灰色，也可以设置为完全透明。
- 支持按法术 ID 手动添加游戏内 Buff，例如狂怒、剑刃乱舞。
- 配置页：可以创建多个页面，并分别设为账号通用或角色专用。
- 将当前配置页导出为短编码字符串，或从字符串导入。
- 界面语言可选：跟随 Hordes of Azeroth、简体中文、English。
- `/wa` 打开配置窗口；拖动图标调整位置，右键取消跟踪。

## 前置条件

- 使用 benilla 客户端的 Hordes of Azeroth。
- Hordes of Azeroth 天赋状态监控需要安装并启用 `HordesOfAzeroth` 插件。真实 Buff 监控不依赖它。

## 安装

1. 从仓库的 Releases 页面下载 `BonkAuras-<版本>.zip`。
2. 把压缩包里的 `BonkAuras` 文件夹解压到游戏的插件目录：

   ```
   <Hordes of Azeroth>/benilla-config/AddOns/BonkAuras
   ```

   确保 `BonkAuras.toc`、`BonkAuras.lua`、`BonkAurasSpells.lua` 直接位于该文件夹内。

3. 重启游戏。如果之前已经安装过 BonkAuras，输入 `/reload` 即可。
4. 输入 `/wa` 打开配置窗口。

## 使用

### 主界面

- **当前玩家 Buff**：点击条目即可开始监控该 Buff。
- **已跟踪**：列出当前所有监控项。右键条目可取消跟踪。
- **手动添加 Buff ID**：输入法术 ID 后点“添加”。例如 `13046`（狂怒）、`13877`（剑刃乱舞）、`1243`（真言术：韧）。
- **显示 Buff ID**：在当前 Buff 列表显示法术 ID，并把 ID 追加到 Buff Tooltip 中。
- **追踪图标 Tooltip**：打开或关闭追踪图标的悬浮提示。
- **未生效**：选择灰色显示，或完全透明。
- **语言**：跟随 Hordes of Azeroth，或强制简体中文 / English。
- **解锁拖动**：解锁后可拖动图标调整位置；右键追踪图标可取消跟踪。
- **清除全部**：移除当前配置页的全部监控项。

### 配置页

在主界面第一行点击 **配置页** 打开管理窗口。

- 点击配置页即可切换。
- **新建**：使用当前页面的设置创建一个空配置页。
- **保存**：保存当前名称和全部设置，包括图标位置；在名称框按回车也可以保存。
- **重命名**：修改当前配置页名称。
- **删除**：删除当前配置页；始终会保留至少一个可用配置页。
- **切换作用域**：在 **账号通用** 和 **角色专用** 之间切换：
  - 账号通用：所有角色都能看到并使用该配置页。
  - 角色专用：只有创建它的角色能看到和使用。
- 切换配置页时也会自动保存当前页。

### 导入与导出

- **导出配置**：弹窗会显示当前配置页的短字符串，以 `BKA1` 开头。打开时默认全选，按 `Ctrl+C` 复制。
- **导入配置**：粘贴字符串后点“导入”，会替换当前配置页的设置和监控项。
- 导入时会忽略空格和换行。

### 默认配置

首次安装时，BonkAuras 会创建一个名为 `Default`（HOA 为中文时为“默认”）的账号通用配置页，包含 5 个 Hordes of Azeroth 状态监控：护盾、冲刺、死疽、受创、决心。

界面语言默认跟随 Hordes of Azeroth，追踪图标 Tooltip 默认关闭。两项都可以在主界面修改。

## 说明

- 1.12.1 客户端不向插件暴露当前 Buff 的真实法术 ID，因此 BonkAuras 使用图标来识别被监控的 Buff。游戏 Buff 上显示的 ID 来自内置的 1.12.1 法术索引；同一图标对应多个法术时显示的是代表 ID，使用该 ID 添加仍会正确监控这个图标。
- Hordes of Azeroth 状态监控依赖服务端下发的 `BONK~` 消息，因此需要安装并启用 `HordesOfAzeroth` 插件。
- 插件只监控玩家自己的 Buff。

## 开发

- `BonkAurasSpells.lua` 由 1.12.1 客户端的 `Spell.dbc` 和 `SpellIcon.dbc` 生成，请勿手动修改。
- 合并到 `main` 的 Pull Request 会运行基础 Lua 语法检查和 TOC 文件检查。
- 推送 `v0.10` 这类标签会打包完整的 `BonkAuras` 插件目录并发布 Release。

## 许可证

MIT，见 [LICENSE](LICENSE)。
