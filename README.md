
## Description

This repository contains a partial implementation of the domain model. It contains unit tests which can be run through pytest. It also contains a simple Flask application that renders content of a Recipe object instance from our domain model on a blank HTML page. You'll be expanding the domain model implementation, and you have the freedom to add, modify or remove test cases as needed.

## Installation

**Installation via requirements.txt**

**Windows**

```shell
$ cd <project directory>
$ py -3 -m venv venv
$ venv\Scripts\activate
$ pip install -r requirements.txt
```

**MacOS**

```shell
$ cd <project directory>
$ python3 -m venv venv
$ source venv/bin/activate
$ pip install -r requirements.txt
```

When using PyCharm, set the virtual environment using 'File or PyCharm'->'Settings' and select your project from the left menu. Select 'Project Interpreter', click on the gearwheel button and select 'Add Interpreter'. Click the 'Existing environment' radio button to select the virtual environment.

## Execution

**Running the application**

From the *project directory*, and within the activated virtual environment (see *venv\Scripts\activate* above):

````shell
$ flask run
````

## Health Star Rating

Per serving, we compute a structured 0–5 Health Star Rating inspired by HSR/traffic-light schemes:

- Negative (baseline) points: energy, saturated fat, sugar, sodium (more → worse)
- Positive adjustment points: fiber, protein (more → better)

Point rules (per serving):

- Energy (kJ): start 600 kJ, +1 point per +200 kJ, max 10
- Saturated fat (g): start 1 g, +1 per +1 g, max 10
- Sugar (g): start 5 g, +1 per +5 g, max 10
- Sodium (mg): start 120 mg, +1 per +120 mg, max 10
- Fiber (g): start 0.9 g, +1 per +1 g, max 5 (positive)
- Protein (g): start 1 g, +1 per +5 g, max 5 (positive)

Final score = negative_points_total − positive_points_total.

Mapping to stars: stars = 5.0 − 0.25 × score, clamped to [0, 5] and rounded to 1 decimal.

If all key fields are missing/zero, we display “Health star rating unavailable”.

## Testing

After you have configured pytest as the testing tool for PyCharm (File - Settings - Tools - Python Integrated Tools - Testing), you can then run tests from within PyCharm by right-clicking the tests folder and selecting "Run pytest in tests".

Alternatively, from a terminal in the root folder of the project, you can also call 'python -m pytest tests' to run all the tests. PyCharm also provides a built-in terminal, which uses the configured virtual environment.

## Configuration

The *project directory/.env* file contains variable settings. They are set with appropriate values.

* `FLASK_APP`: Entry point of the application (should always be `wsgi.py`).
* `FLASK_ENV`: The environment in which to run the application (either `development` or `production`).
* `SECRET_KEY`: Secret key used to encrypt session data.
* `TESTING`: Set to False for running the application. Overridden and set to True automatically when testing the application.
* `WTF_CSRF_SECRET_KEY`: Secret key used by the WTForm library.

## Data sources

The data files are modified excerpts downloaded from:

https://www.kaggle.com/datasets/irkaal/foodcom-recipes-and-reviews/
