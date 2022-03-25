# everything-recognition

This script uses [OpenCV](https://opencv.org/) recognition library to recognize everything!.. Well, okay. Maybe it's not *actually* everything, but still - an impressive list of entities.

With defalut configuration you can expect, that:

- Faces
- Eyes
- Smiles
- Human bodies
- CAT FACES (!)

are going to be surrounded by colorful bounding boxes, for as long as they are in your webcam video feed. 

However, some of these options are switched off by default, so make sure to check **Basic setup** section if you want to detect 'dem cat faces!

## Installation guidelines

You must have Python3 installed on your system.
You may use `pip` (or `pip3` to avoid conflict with Python2) to install dependencies.
```
pip install -r requirements.txt
```
It is strongly advised to use [virtualenv/venv](https://docs.python.org/3/library/venv.html) for project isolation.

## Basic setup

As stated above, this script relies on Python implementation of OpenCV recognition library. For the actual detection to take place, you'll need a special type of recognition model, known as `Haar Cascade Classifier`.

No worries! You won't need to build and train your own models, as there are plenty of freely avaliable resources for that sort of thing, and some of the are already included in this repository (you can find them in `./haarcascades` folder).

*Haar Cascades* which are used by the script are defined in `config.py` file. Let's take a look at it:

```Python
CASCADES = {
    "Face front": {
        "path": "haarcascades/faces/haarcascade_frontalface_default.xml",
        "color": (255, 0, 0),
        "draw": True
    },
    "Face profile": {
        "path": "haarcascades/faces/haarcascade_profileface.xml",
        "color": (255, 0, 0),
        "draw": True
    },
    "Smile": {
        "path": "haarcascades/faces/haarcascade_smile.xml",
        "color": (0, 255, 0),
        "draw": False
    },
    "Eyes": {
        "path": "haarcascades/faces/haarcascade_eye.xml",
        "color": (0, 255, 0),
        "draw": True
    },
    "Full body": {
        "path": "haarcascades/faces/haarcascade_fullbody.xml",
        "color": (0, 255, 0),
        "draw": False
    },
    "Cat face": {
        "path": "haarcascades/faces/haarcascade_frontalcatface_extended.xml",
        "color": (0, 255, 0),
        "draw": False
    }
}
```

As you can see, each avaliable cascade is identified by a name, and defined by a set of parameters:

- `path` specifies a path to the special descriptor file of *Haar Cascade* model. These are `.xml` files in your `./haarcascade` folder.
- `color` specifies RGB color of the bounding box, which is going to be drawn on detection.
- `draw` is a flag, that you can use to easily include/omit the model from calculation. You may notice, that in the given configuration `Smile`, `Full body` and `Cat face` models are omitted.

Normally, you can have as many cascades as you want to be used in detection, but consider, that each single cascade calculation is a resource intensive operation. So it is highly advised to omit models that are not required for your detection purposes.

BTW, you also need a webcam. 

## Basic usage

Once you have your `config.py` setup and your webcam connected, just use the command:

```
python run.py
```

You will see a window with your webcam video feed. Once something is detected it will be highlighted by a bounding box of predefined color. 

Have fun!
