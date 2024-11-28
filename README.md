### 关于 Read the Docs

1. **文档生成工具**：
   - **Sphinx**：Read the Docs 最常用于托管 Sphinx 生成的文档。Sphinx 是一个强大的文档生成工具，支持 reStructuredText 标记语言。
   - **MKDocs**：另一种常用的文档生成工具，支持 Markdown 标记语言。
2. **主要特点**：
   - **自动构建**：Read the Docs 可以自动从版本控制系统（如 GitHub、GitLab、Bitbucket）拉取文档源文件并生成 HTML 文档。
   - **多版本支持**：支持多个文档版本，方便用户查看不同版本的文档。
   - **搜索功能**：提供内置的全文搜索功能，帮助用户快速查找内容。
   - **自定义主题**：支持自定义文档主题，可以调整文档的外观。
   - **API 文档集成**：支持与 API 文档生成工具（如 Swagger、Doxygen）集成。

### 如何使用 Read the Docs

1. **注册账户**：
   - 访问 [Read the Docs](https://readthedocs.org/?spm=5176.28103460.0.0.55275d276Lx9D8) 并注册一个账户。
2. **连接仓库**：
   - 登录后，连接你的版本控制系统（如 GitHub）。
   - 选择你要托管文档的仓库。
3. **配置文档**：
   - 在仓库中添加必要的配置文件，如 `docs/` 目录下的 `conf.py` 文件（用于 Sphinx）。
   - 配置 Read the Docs 以使用正确的构建命令和输出目录。
4. **自动构建**：
   - 一旦配置完成，Read the Docs 会自动从仓库中拉取最新的文档源文件并生成 HTML 文档。
   - 你可以在 Read the Docs 的管理界面中查看构建状态和日志。
5. **发布文档**：
   - 文档生成后，可以通过 Read the Docs 提供的 URL 访问。
   - 例如，`https://google-cartographer.readthedocs.io/en/latest/pbstream_migration.html` 就是通过 Read the Docs 托管的文档页面。

```c
# Read the Docs configuration file for Sphinx projects
# See https://docs.readthedocs.io/en/stable/config-file/v2.html for details

# Required
version: 2

# Set the OS, Python version and other tools you might need
build:
  os: ubuntu-22.04
  tools:
    python: "2.7"
    # You can also specify other tool versions:
    # nodejs: "20"
    # rust: "1.70"
    # golang: "1.20"

# Build documentation in the "docs/" directory with Sphinx
sphinx:
  configuration: docs/source/conf.py
  # You can configure Sphinx to use a different builder, for instance use the dirhtml builder for simpler URLs
  # builder: "dirhtml"
  # Fail on all warnings to avoid broken references
  # fail_on_warning: true

# Optionally build your docs in additional formats such as PDF and ePub
# formats:
#   - pdf
#   - epub

# Optional but recommended, declare the Python requirements required
# to build your documentation
# See https://docs.readthedocs.io/en/stable/guides/reproducible-builds.html
# python:
#   install:
#     - requirements: docs/requirements.txt
```



### 示例配置

假设你使用 Sphinx 生成文档，以下是一个简单的 `conf.py` 配置文件示例：

```python
# conf.py

import os
import sys
sys.path.insert(0, os.path.abspath('..'))

# -- Project information -----------------------------------------------------

project = 'Google Cartographer'
copyright = '2022, The Cartographer Authors'
author = 'The Cartographer Authors'

# -- General configuration ---------------------------------------------------

extensions = [
    'sphinx.ext.autodoc',
    'sphinx.ext.viewcode',
    'sphinx.ext.todo',
]

templates_path = ['_templates']
exclude_patterns = ['_build', 'Thumbs.db', '.DS_Store']

# -- Options for HTML output -------------------------------------------------

html_theme = 'sphinx_rtd_theme'
html_static_path = ['_static']
```





```bash

git clone --no-single-branch --depth 50 https://github.com/cartographer-project/cartographer . 
git checkout --force origin/master 
git clean -d -f -f 
python2.7 -mvirtualenv  
python -m pip install --upgrade --no-cache-dir pip setuptools<58.3.0 
python -m pip install --upgrade --no-cache-dir pillow mock==1.0.1 alabaster>=0.7,<0.8,!=0.7.5 commonmark==0.9.1 recommonmark==0.5.0 sphinx<2 sphinx-rtd-theme<0.5 readthedocs-sphinx-ext<2.2 jinja2<3.1.0 
python -m sphinx -T -E -b html -d _build/doctrees -D language=en . _build/html 
python -m sphinx -T -E -b readthedocssinglehtmllocalmedia -d _build/doctrees -D language=en . _build/localmedia 
python -m sphinx -b latex -D language=en -d _build/doctrees . _build/latex 
cat latexmkrc 
latexmk -r latexmkrc -pdf -f -dvi- -ps- -jobname=google-cartographer -interaction=nonstopmode 
mv -f docs/source/_build/latex/google-cartographer.pdf sphinx_pdf/google-cartographer.pdf 
python -m sphinx -T -E -b epub -d _build/doctrees -D language=en . _build/epub 
mv -f docs/source/_build/epub/Cartographer.epub sphinx_epub/google-cartographer.epub 


git clone --depth 1 https://github.com/cloudflyMa/test_doc.git . 
git fetch origin --force --prune --prune-tags --depth 50 refs/heads/master:refs/remotes/origin/master 
git checkout --force origin/master 
cat .readthedocs.yaml 
asdf global python 3.12.7 
python -mvirtualenv $READTHEDOCS_VIRTUALENV_PATH 
python -m pip install --upgrade --no-cache-dir pip setuptools 
python -m pip install --upgrade --no-cache-dir sphinx 
python -m sphinx -T -b html -d _build/doctrees -D language=en . $READTHEDOCS_OUTPUT/html 
```



```txt
git clone --no-single-branch --depth 50 https://github.com/cartographer-project/cartographer . 
git checkout --force 105c034577220268cd28a304a185adbec46b729f 
git clean -d -f -f 
python2.7 -mvirtualenv  
python -m pip install --upgrade --no-cache-dir pip setuptools 
python -m pip install --upgrade --no-cache-dir  mock==1.0.1 pillow==5.4.1 alabaster>=0.7,<0.8,!=0.7.5 commonmark==0.8.1 recommonmark==0.5.0 sphinx<2 sphinx-rtd-theme<0.5 readthedocs-sphinx-ext<2.2 
python -m sphinx -T -b html -d _build/doctrees -D language=en . _build/html 
python -m sphinx -T -b readthedocssinglehtmllocalmedia -d _build/doctrees -D language=en . _build/localmedia 
python -m sphinx -b latex -D language=en -d _build/doctrees . _build/latex 
cat latexmkrc 
latexmk -r latexmkrc -pdf -f -dvi- -ps- -jobname=google-cartographer -interaction=nonstopmode 
mv -f docs/source/_build/latex/google-cartographer.pdf sphinx_pdf/google-cartographer.pdf 
python -m sphinx -T -b epub -d _build/doctrees -D language=en . _build/epub 
mv -f docs/source/_build/epub/Cartographer.epub sphinx_epub/google-cartographer.epub
```

