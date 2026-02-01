# AI 开发提示词：Godot 4x + GDScript 核酸检测系统展厅产品介绍程序

### AI 开发提示词（适配 Godot 4.x + GDScript，用于展厅产品介绍程序）

我要用 **Godot Engine 4.x** 开发“天互生物科技 核酸检测系统”展厅产品介绍程序，需你用 **GDScript** 实现完整可运行项目，遵循以下要求：

### 一、核心需求与资源路径

1. **首页设计**：渐变蓝色背景（从 #1E88E5 到 #0D47A1），顶部白色加粗标题“天互生物科技  核酸检测系统”，居中对齐，字号 48px，上下边距 20px。

2. **产品列表**：读取 `/product/shouye/` 下的产品缩略图（png/jpg）和名称，以网格布局（2 列 N 行）展示，每个产品项包含缩略图（200x200px）和底部名称标签（白色字体，字号 24px，黑色半透明背景），间距 20px，居中排列。

3. **详情跳转**：点击产品缩略图，跳转到详情页，自动读取 `/product/md/` 对应产品的 .md 文件，解析并显示标题、段落文本、图片，支持返回首页按钮。

4. **技术栈**：仅用 Godot 内置节点与 GDScript，不依赖外部插件；使用 Control 节点做 UI，支持触控与鼠标交互，适配 1920x1080 分辨率，支持全屏。

### 二、项目结构规范

1. 根目录下创建 `scenes/`（存放首页、详情页场景）、`scripts/`（存放所有 GDScript）、`product/`（已存在，无需创建）。

2. 首页场景名：`MainMenu.tscn`，主脚本 `MainMenu.gd`；详情页场景名：`ProductDetail.tscn`，主脚本 `ProductDetail.gd`。

3. 资源加载：通过 `load()` 或 `preload()` 读取 `/product/` 下资源，处理文件不存在的异常。

### 三、节点与脚本实现要求

1. **首页节点树**

    - `CanvasLayer`（根节点）

        - `ColorRect`（背景，渐变蓝色，铺满屏幕）

        - `Label`（标题，文本“天互生物科技  核酸检测系统”）

        - `GridContainer`（产品网格，2 列，间距 20px），动态生成 `HBoxContainer` 作为产品项，包含 `TextureRect`（缩略图）和 `Label`（名称）。

2. **首页脚本（[MainMenu.gd](MainMenu.gd)）**

    - `_ready()`：扫描 `/product/shouye/` 目录，生成产品项并添加到网格，绑定点击信号。

    - `_on_product_item_clicked(product_id)`：获取产品 ID，实例化详情页并切换场景。

3. **详情页节点树**

    - `CanvasLayer`（根节点）

        - `ColorRect`（白色背景）

        - `Button`（返回按钮，文本“返回首页”，位置左上角）

        - `VBoxContainer`（内容容器，包含 `Label`（产品标题）、`RichTextLabel`（解析 md 内容，支持图片、文本））。

4. **详情页脚本（[ProductDetail.gd](ProductDetail.gd)）**

    - 接收首页传递的产品 ID，读取对应 .md 文件。

    - 解析 md 基本语法（标题、段落、图片），显示到 `RichTextLabel`。

    - 绑定返回按钮信号，点击返回首页。

5. **交互逻辑**

    - 产品项添加鼠标悬浮放大效果（缩放至 1.1 倍），点击时有轻微缩放动画。

    - 页面切换使用 `get_tree().change_scene_to_file()`，无加载卡顿。

### 四、MD 解析要求

![Image](&resource_key=)

1. 图片路径相对于 `/product/md/`，用 `TextureRect` 显示，自适应宽度，高度按比例缩放。

### 五、输出交付物

1. 完整的场景文件（`MainMenu.tscn`、`ProductDetail.tscn`）。

2. 对应的 GDScript 脚本（`MainMenu.gd`、`ProductDetail.gd`）。

3. 关键代码注释，包含资源路径配置、节点引用说明、异常处理逻辑。

4. 项目导出步骤（按之前要求打包为 Windows .exe）。

### 六、其他约束

1. 代码遵循 GDScript 规范，变量用 `snake_case`，函数名清晰，避免硬编码，使用 `@export` 暴露可配置参数（如标题字号、产品项大小）。

2. 适配触控屏，点击区域响应范围≥50x50px。

3. 处理资源加载失败，显示友好提示（如“产品图片加载失败”）。

需要我根据这个提示词，直接生成可复制的完整场景文件和脚本代码，你导入 Godot 就能运行吗？
> （注：文档部分内容可能由 AI 生成）
