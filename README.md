# Mindcuber-Python
A program written in python3 (3.9) that solves a Rubik's cube with a ev3 Mindstorms, without needing a SD card.

Very easy to setup. Just follow the steps.

You need to build the mindcuber robot. The "MindCub3r-v1p0.pdf" file has the building instructions (You can also find them  at https://www.mindcuber.com).

The motor of the arm should connect to the A Port.
The motor of the platform should connect to the B Port.

Don't mind connecting the other cables. This program doesnt use them.

See this to connect your pc with the ev3 (Bluetooh does not work for MacOS) - https://ev3-dc.readthedocs.io/en/latest/examples_ev3.html#connect-with-the-ev3-device
(I strongly recommend USB)
### Table of contents
1. Installation
2. Setup
3. Run
4. Manual install (Use this if automatic fails)

## Installation

```
$ pip install git+https://github.com/PBeGood4/mindcuber-python
 # This will install all dependecies
 # opencv-python might take a while


 # If you already have opencv-python installed, you can do this instead
$ pip install git+https://github.com/PBeGood4/mindcuber-python@no-opencv
```

## Setup

**Open mindcuber-python.py**

To find this file:

### MacOS / Linux

```
which mindcuber-python.py
```

### Windows

```
where mindcuber-python.py
```

**Go to `ev3Device = ev3.EV3(protocol=ev3.USB, host='00:16:53:3D:F8:DF')`**

**Change `ev3.USB` To the protocol you want: `ev3.USB`, `ev3.BLUETOOTH` or `ev3.WIFI`** (I strongly recommend USB)

**Change `host='00:16:53:3D:F8:DF'` to your ev3's MAC adress** (Find the MAC adr in: Brick Info / ID).

 






**To run the program:**

```
$ rubik.py 
```


If it doesnt work, try the manual setup. 

Don't be afraid to open an *issue*.


## Manual setup (Uses this if automatic fails)

**You need admin/root privileges for this (Unless your python environment is local)**

Run:

```
$ rubiks-cube-tracker.py --webcam 0
  # ^^^ this will print alot of things in the console. Look for something like BLBUUDRRFDRUURRRBRBBLLFRLLFUDDUDDDDUUFDLLULBFRBLFBFFFB
  
$ python3 mindcuber-python.py BLBUUDRRFDRUURRRBRBBLLFRLLFUDDUDDDDUUFDLLULBFRBLFBFFFB
  #Instead of "mindcuber-python", write the full path of it
```

This is fine, but not good enough. Let's automate it!


1. Go to **site-packages** of your version of python (The commands bellow should help you find it).
```
# Linux
$ python3 -c "import sysconfig; print(sysconfig.get_path('purelib'))"
/usr/local/lib/python3.8/site-packages

# macOS (brew installed python3.8)
$ python3 -c "import sysconfig; print(sysconfig.get_path('purelib'))"
/usr/local/Cellar/python@3.8/3.8.3/Frameworks/Python.framework/Versions/3.8/lib/python3.8/site-packages

# Windows
C:\> py -c "import sysconfig; print(sysconfig.get_path('purelib'))"
C:\Users\wim\AppData\Local\Programs\Python\Python38\Lib\site-packages
```

2. Open the folder "rubikscubetracker"
3. Open \__init\__.py
4. Search for "kociemba_string"
<img width="783" alt="Screenshot 2021-04-27 at 17 03 15" src="https://user-images.githubusercontent.com/82064173/116274326-796d7f80-a77a-11eb-9296-4f65b016f07a.png">
5. Add the following:

```python3
import subprocess
subprocess.Popen("python3 path_to_mindcuber-python.py " + kociemba_string, shell=True)
                            #^^^ again, write the full path
```

<img width="852" alt="Screenshot 2021-04-27 at 17 05 31" src="https://user-images.githubusercontent.com/82064173/116274671-c81b1980-a77a-11eb-8cf1-6325ce6b7a07.png">

6. Just run:

```
$ rubiks-cube-tracker.py --webcam 0
```

This will get the colors and start solving the cube.

Pretty nice, right?


Any questions, just open up an *issue*. I'll anwser as fast as possible.

Hope this helped :)
