疑惑pip install 和conda install有什么区别?
结论：优先使用conda install
记录下知乎上的回答：

今天正好用到这部分的内容，做一些简单总结，欢迎大家指正：conda install xxx：这种方式安装的库都会放在anaconda3/pkgs目录下，这样的好处就是，当在某个环境下已经下载好了某个库，再在另一个环境中还需要这个库时，就可以直接从pkgs目录下将该库复制至新环境而不用重复下载。pip install xxx：分两种情况，一种情况就是当前conda环境的python是conda安装的，和系统的不一样，那么xxx会被安装到anaconda3/envs/current_env/lib/python3.x/site-packages文件夹中，如果当前conda环境用的是系统的python，那么xxx会通常会被安装到~/.local/lib/python3.x/site-packages文件夹中这里引出一个问题：conda和pip安装同一个xxx库情况下，conda环境下python代码中import xxx时，谁安装的xxx优先级较高会被import，这个问题通过下面这条命令可以解决：python -m site在我的机器上，会有类似下面输出：(py3.6) [~/anaconda3/pkgs @ s64]$ python -m site
sys.path = [
    '~/anaconda3/pkgs',
    '~/anaconda3/envs/py3.6/lib/python36.zip',
    '~/anaconda3/envs/py3.6/lib/python3.6',
    '~/anaconda3/envs/py3.6/lib/python3.6/lib-dynload',
    '~/anaconda3/envs/py3.6/lib/python3.6/site-packages',
]
USER_BASE: '~/.local' (exists)
USER_SITE: '~/.local/lib/python3.6/site-packages' (doesn't exist)
ENABLE_USER_SITE: True这里的USER_BASE 和USER_SITE其实就是用户自定义的启用Python脚本和依赖安装包的基础路径，从上面的输出可以看到，import xxx时，先找的是anaconda3/pkgs目录，所以conda安装的包会被import进来。


作者：月踏
链接：https://www.zhihu.com/question/395145313/answer/2449421755
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
