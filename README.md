# Frontend Adaptation Spec

前端项目统一适配规范 Skill —— 覆盖移动端 H5 与 PC 端，符合 agentskills.io 开放规范，兼容所有主流 AI Agent 框架。

## 快速安装

### 方式一：Skills.sh CLI（推荐）
```bash
npx skills add sumcourage/frontend-adaptation-spec
```

### 方式二：手动安装
将整个文件夹复制到你的 AI Agent 的 skills 目录即可。

## 适配能力

| 平台 | 方案 | 覆盖内容 |
|------|------|----------|
| 移动端 H5 | vw / rem / rpx | viewport meta、安全区域、1px 边框、CSS Reset、PostCSS 配置 |
| 微信/支付宝小程序 | rpx / upx | 原生适配、安全区域、固定底部 |
| PC 端后台 | px + CSS 变量 | 响应式断点（1920+/1440/1280/1024）、字体栈、滚动条美化、布局规范 |

## 目录结构

```
frontend-adaptation-spec/
├── SKILL.md                  # 核心指令（触发条件、执行流程、方案决策树）
├── references/
│   ├── mobile-spec.md        # 移动端完整规范
│   ├── pc-spec.md            # PC 端完整规范
│   └── checklist.md          # 双端适配自查清单
└── assets/
    ├── mobile/
    │   ├── reset.css         # 移动端 CSS Reset
    │   ├── common.css        # 移动端公共样式
    │   └── utils.css         # 移动端工具类
    └── pc/
        ├── reset.css         # PC 端 CSS Reset
        ├── common.css        # PC 端公共样式（含 CSS 变量体系）
        └── utils.css         # PC 端工具类
```

## 兼容的 AI Agent 框架

Claude Code / Cursor / Codex / GitHub Copilot / OpenCode / Windsurf / Cline / Gemini CLI / Pi 等所有支持 SKILL.md 规范的框架。

## 规范来源

基于 agentskills.io 开放规范（SKILL.md），被 Skills.sh（Vercel + Anthropic）、SkillsMP、ClawHub、LobeHub 等主流平台共同采用。

## 许可

CC0-1.0（完全放弃署名，可自由使用/修改/商用）
