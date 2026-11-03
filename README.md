# 日记 · 打卡

一个单页应用：写待办、打卡、计时。可安装到手机桌面（PWA），支持离线。

## 文件说明

| 文件 / 目录 | 作用 |
| --- | --- |
| `index.html` | 整个应用（HTML + CSS + JS + 标题图），单文件 |
| `manifest.json` | PWA 配置：应用名、图标、独立窗口 |
| `sw.js` | 离线缓存 |
| `icons/` | 桌面图标 |
| `wallpapers/` | 可选的内置壁纸（预设） |
| `.nojekyll` | 告诉 GitHub Pages 不要用 Jekyll 处理 |

## 部署到 GitHub Pages

1. 打开 https://github.com 注册账号
2. 右上角 **+** → **New repository**
   - Repository name：`diary`（随便起，会进网址）
   - 选 **Public**（免费版私有仓库不能用 Pages）
   - 不要勾 "Add a README file"
   - **Create repository**
3. 仓库 → **Add file** → **Upload files**
   把本文件夹里的**全部内容**拖进去（`icons`、`wallpapers` 一起拖，保持结构）
   → **Commit changes**
4. 仓库 → **Settings** → 左侧 **Pages**
   - Source：**Deploy from a branch**
   - Branch：**main**，目录 **/ (root)**
   - **Save**
5. 等 1~2 分钟，网址是 `https://你的用户名.github.io/diary/`
6. 手机打开 → 分享 → **添加到主屏幕**

## 壁纸怎么用

分两种，互不影响：

**① 自己的照片（推荐，不用碰 GitHub）**

在 App 里「我的 → 背景图 → 选图片」，直接从手机相册挑。图片存在手机的 IndexedDB 里，容量通常几百 MB，加多少张都行，只有你自己这台设备能看到。

**② 内置预设（可选）**

`wallpapers/` 里的那几张渐变图属于站点自带的，所有人打开都能看到。想增加预设才需要传 GitHub：

- 按 `1.jpg`、`2.jpg`、`3.jpg` 顺序编号，**不要断号**
- 传进仓库的 `wallpapers` 文件夹，手机打开「我的」页就会自动出现
- 不用改任何配置文件

> 也可以用任意文件名：放一个 `wallpapers/index.json`，内容是文件名数组（如 `["sea.jpg","night.jpg"]`），程序会优先按它加载。

**区别**：内置的换了手机还在；自己传的只在那台手机的那台浏览器里，清缓存或换手机就没了。

## 注意

- 日记、打卡、待办存在 localStorage，壁纸存在 IndexedDB，**都按网址隔离**。换网址等于从零开始。
- 「我的 → 导出数据」可把日记等记录复制成 JSON 备份（壁纸不包含在内）。
- 改了页面，把 `sw.js` 顶部 `CACHE = "diary-v1"` 的版本号 +1，否则手机可能读旧缓存。
