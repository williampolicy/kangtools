# kangtools
kangtools

- git remote
- renew verison.
- upload add date. 


创建并发布自己的Python包到PyPI需要以下步骤：

1. **项目结构**：在你的项目目录下创建以下文件和目录结构：

   ```
   your_project/
   ├── your_package/
   │   ├── __init__.py
   │   ├── your_module.py  # 将你的版本控制代码放在这个文件里
   ├── setup.py
   ├── README.md
   ├── LICENSE
   ```

   其中，`your_package` 是你的Python包的名字，`your_module` 是模块的名字。`__init__.py` 是一个必需的空文件，它告诉Python这个目录是一个包。

2. **`setup.py` 文件**：这个文件用于定义你的包的元数据，包括包的名字，版本，作者，许可证等。下面是一个例子：

   ```python
   from setuptools import setup

   setup(
       name='your-package',  # 包的名字
       version='0.0.1',  # 包的版本
       author='Your Name',  # 你的名字
       author_email='your.email@example.com',  # 你的邮箱
       packages=['your_package'],  # 包含的包，这是一个列表，如果你的项目包含多个包，都需要列在这里
       license='LICENSE',  # 许可证文件
       description='A Python package for version control.',  # 包的简短描述
       long_description=open('README.md').read(),  # 包的详细描述，通常从 README.md 文件读取
       long_description_content_type="text/markdown",  # 描述的格式，使用markdown格式
   )
   ```

3. **`README.md` 和 `LICENSE` 文件**：`README.md` 文件包含了你的包的详细信息和使用方法。`LICENSE` 文件包含了你的包的许可证信息。

4. **注册PyPI账户**：访问 https://pypi.org/ 并注册一个账户。

5. **安装工具**：使用pip安装 `twine`，`wheel` 和 `setuptools`，这些工具用于构建和上传你的包：

   ```bash
   pip install twine wheel setuptools
   ```

6. **构建包**：在你的项目目录下运行以下命令，它会创建 `dist/` 目录，并在该目录下生成你的包的源码和wheel格式的发行版本：

   ```bash
   python setup.py sdist bdist_wheel
   ```

7. **上传包**：使用 `twine` 将你的包上传到PyPI：

   ```bash
   twine upload dist/*
   ```

   这时你需要输入你的PyPI账户的用户名和密码。

8. **安装包**：现在你就可以使用pip从PyPI安装你的包了：

   ```bash
   pip install your-package
   ```

   你需要将 `your-package` 替换为你的包的名字。

以上就是创建并发布Python包到PyPI的基本流程。请注意，每次发布新的版本时，需要在 `setup.py` 文件中更新版本号，然后重新


pip install twine wheel setuptools



您可以将 `version_control.py` 作为一个命令行工具来使用，有两种方法可以实现这一点。

1. **在python文件中添加shebang行：** 在你的 `version_control.py` 文件的最顶端添加一行 `#!/usr/bin/env python3`，这是一个指定解释器的shebang。然后你需要给这个文件添加执行权限，你可以使用 `chmod +x version_control.py` 命令来做这件事。这样你就可以像一个脚本一样运行它了，例如 `./version_control.py`。

2. **将python代码封装为命令行工具：** Python 提供了一些库如 argparse, click 可以帮助你创建自己的命令行工具，然后你可以在 `setup.py` 中使用 `entry_points` 来指定这个工具的名字和对应的函数。

示例:

在 `setup.py` 中添加以下代码:

```python
entry_points={
    'console_scripts': [
        'kangtools_version_control=kangtools.version_control:main',
    ],
},
```

然后你需要在 `version_control.py` 中添加一个 `main` 函数，把上面的代码封装在这个函数里。`main` 函数可以接收命令行参数。例如:

```python
def main():
    # your existing code goes here...
    ...

if __name__ == "__main__":
    main()
```

现在你可以重新安装你的包，然后你可以在任何地方使用 `kangtools_version_control` 这个命令行工具了。例如:

```bash
kangtools_version_control
```

这将会运行 `version_control.py` 文件中的 `main` 函数。

-----
