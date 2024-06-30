Installing Sphinx
==========================
Sphinx 是一个 Python 应用程序。它可以通过下述方式之一安装。

PyPI package
~~~~~~~~~~~~~~
Sphinx 包发布在 Python 包索引 (PyPI) 上。从 PyPI 安装包的首选工具是 pip，它包含在所有现代版本的 Python 中。

运行以下命令：
pip install -U sphinx

为了避免重建环境时出现问题，建议将 sphinx 和第三方扩展版本固定在 requests.txt 文件中：
`pip freeze > requirements.txt`。

`pip install -r requirements.txt`


