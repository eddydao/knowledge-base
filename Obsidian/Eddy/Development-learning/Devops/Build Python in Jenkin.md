Python script run in Windows with Jenkins freestyle:
```bash
cd %WORKSPACE%

  

python -m venv venv

  

call venv\Scripts\activate.bat

  

pip install --upgrade pip

pip install -r requirements.txt

  

set FLASK_APP=app.py

set FLASK_ENV=development

  

:: Run Flask inside activated venv

python -m flask run --host=0.0.0.0 --port=5000
```



