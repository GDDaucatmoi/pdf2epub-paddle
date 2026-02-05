# Scanned PDF to Epub Converter (扫描版 PDF 转 EPUB)

[English](README.md) | [中文](README_zh.md)

本工具利用百度 PaddleOCR 版面分析 API，将扫描版 PDF 书籍转换为清晰、易读的 EPUB 电子书。

## 功能特性

- **高质量版面分析**：使用 PaddleOCR 智能识别段落、标题、图片和表格。
- **智能章节分割**：根据标题（如“第一章”、“Part I”）自动将书籍分割为不同章节。
- **保留图片**：完整保留原 PDF 中的图片。
- **纯净输出**：自动移除页眉、页脚和页码，提供无缝阅读体验。
- **高鲁棒性**：
  - **断点续传**：每处理完一个分块自动保存进度。如果中断，重新运行即可从断点处继续。
  - **速率限制**：内置延时以遵守 API 调用频率限制。
  - **自动重试**：遇到 API 请求失败时自动重试。

## 前置要求

- Python 3.8+
- PaddleOCR API Token（从 [百度飞桨星河社区 (AIStudio)](https://aistudio.baidu.com/) 获取）

## 获取 API Token

1. 登录 [百度飞桨星河社区 (AIStudio)](https://aistudio.baidu.com/)。
2. 进入 **“应用中心”** 或 **“在线模型”** 版块（寻找版面分析/Layout Parsing 相关服务）。
3. 找到 **“PaddleOCR”** 或 **“文档分析”** API。
4. 在个人中心或应用设置中复制你的私有 **API Token**。
    *注意：请确保你的账户有足够的调用额度（页数/天）。*

## 安装与使用 (推荐使用 `uv`)

本项目使用 [uv](https://github.com/astral-sh/uv) 进行快速、可靠的依赖管理。

1. **克隆仓库**：

    ```bash
    git clone https://github.com/yourusername/pdf2epub-paddle.git
    cd pdf2epub-paddle
    ```

2. **安装 `uv`** (如果你尚未安装)：

    ```bash
    # macOS/Linux
    curl -LsSf https://astral.sh/uv/install.sh | sh
    ```

3. **使用 `uv` 直接运行** (自动处理虚拟环境和依赖)：

    ```bash
    export PADDLE_API_TOKEN='你的api_token'
    uv run pdf2epub_paddle.py /path/to/your/book.pdf
    ```

### 替代方案：使用标准 Pip

如果你更习惯使用标准 pip：

1. 创建虚拟环境：

    ```bash
    python -m venv .venv
    source .venv/bin/activate
    ```

2. 安装依赖：

    ```bash
    pip install .  # 根据 pyproject.toml 安装
    ```

3. 运行：

    ```bash
    export PADDLE_API_TOKEN='你的api_token'
    python pdf2epub_paddle.py /path/to/your/book.pdf
    ```

## 配置项

- **Chunk Size (分块大小)**：默认为每块 5 页，以确保稳定性。如果你的网络连接稳定且额度较高，可以在脚本中修改 `CHUNK_SIZE`。
- **Timeout (超时时间)**：默认请求超时时间为 180 秒。

## 开源协议

[MIT License](LICENSE)
