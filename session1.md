# Setup your environment
If you start your new job as a software developer, what you need to do on day 1 is to set up your environment. The developing environment can mean a lot of things for an experienced developer. But since you are a newbee, I guess what your new boss minimal expectation is **to let the codebase run on your machine**.

Pick your python distribution
---
There are two popular choices: [Python](https://www.python.org/) and [Anaconda](https://www.anaconda.com/). From my personal experiences, if you use linux or MacOS, take [Python](https://www.python.org/); if you use windows, take [Anaconda](https://www.anaconda.com/).

If you use linux or MacOS, you can solve everything in terminal, install [Python](https://www.python.org/), it is light weight and nothing hiden inside. Therefore, I recommend you just build things from it.

If you are on the darkside, sometimes things can become very tricky. If you don`t want to get your hands dirty, [Anaconda](https://www.anaconda.com/) can make things easier.
 
**BUTTT** for linux and MacOS user you don't need to do anything!!! because you already have python in your system. You might ask, what if your project is built on `Python 3.6` but your system is `Python 2.7`. Don't worry please wait I will tell you what to do.

To verify your installation works, do the following in terminal or cygwin  or whatever.
```cmd
python
```
it will print out
```cmd
Python 3.6.6 (default, Jun 28 2018, 04:42:43) 
[GCC 5.4.0 20160609] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

or
```cmd
which python
```

it will print out
```cmd
/usr/bin/python
```

If you see things similiar to those, you are good for the next step.


Don`t put stuff in your root environment
---
After setting up python, you cannot resist to run the codebase or any project you find online. Then you realise it requires many packages. For example you receive this error:

```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'pytorch'
```

This error means, you need to install a package called `pytorch`. However, **do not do this for your root environment**. Your python root environment is fresh and clean after you just installed it on your machine.

To create a **virtual environment** is what a professional developer will do.

## 1. Plain Python ([virtualenv](https://virtualenv.pypa.io/en/stable/userguide/))
If you use plain Python, below are the instructions for you!

* First install virtualenv
```cmd
pip install virtualenv
```

* Create a `python3` virtualenv called `test_env`
```
virtualenv -p python3 test_env
```

* Use this virtualenv `test_env`
```
source test_env/bin/activate
```

Then you will see something like this:
```
(test_env) jiajuns@jiajuns-desktop:~$ 
```

Now, you are in your `test_env` environment. When you run `python` in this mode, you are not using your root python. The benfit will show up when you are working with different project and each of them has unique environment. Also if you f**k up your environment, you can just delete it and create it again. Image what will happen if your root environment broke, that is the real pain.

## 2. Anaconda
Anaconda has create tools to create conda environment, which works like `virtualenv`