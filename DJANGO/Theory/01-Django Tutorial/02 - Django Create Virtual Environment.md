

---

## Setting Up a Virtual Environment

It's recommended to create a dedicated virtual environment for each Django project. One way to manage virtual environments is using [venv](https://docs.python.org/3/tutorial/venv.html), which is included with Python.

### Creating the Virtual Environment

You can name your virtual environment anything you like; in this tutorial, we'll name it `myworld`. First, navigate to the directory where you want to create your project, then run the following commands:

**Windows:**

```bash
py -m venv env
```

**Unix/MacOS:**

```bash
python3 -m venv env
```

This will set up a virtual environment and create a folder named `myworld` with the following structure:

```
myworld  
  Include  
  Lib  
  Scripts  
  pyvenv.cfg
```

### Activating the Virtual Environment

To activate the virtual environment, use the following commands:

**Windows:**

```bash
myworld\Scripts\activate.bat
```

**Unix/MacOS:**

```bash
source myworld/bin/activate
```

Once activated, your command prompt will change to indicate that the virtual environment is active:

**Windows:**

```bash
(myworld) C:\Users\YourName\>
```

**Unix/MacOS:**

```bash
(myworld) ... $
```

**Note:** You need to activate the virtual environment every time you open a new command prompt or terminal session to work on your project.

---

