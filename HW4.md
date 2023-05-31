HW4
```
Задание: необходимо создать Dockerfile, основанный на любом образе (вы в праве выбрать самостоятельно).
В него необходимо поместить приложение, написанное на любом известном вам языке программирования (Python, Java, C, С#, C++).
При запуске контейнера должно запускаться самостоятельно написанное приложение.
```

```
cd ~

mkdir python-docker

sudo apt install python3.10-venv

cd python-docker

python3 -m venv .venv

source .venv/bin/activate

python3 -m pip install Flask

python3 -m pip freeze > requirements.txt

touch app.py
nano app.py
***
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, Docker!'
***

Проверяем работоспособность: 
python3 -m flask run
В браузере заходим на localhost:5000

Создаем Dockerfile:
cd python-docker/
nano Dockerfile
***
# Базовый образ.

FROM python:3.8-slim-buster

# Указываем или создаём новую рабочую директорию контейнера.

WORKDIR /app

# Копируем файл в текущую рабочую директорию образа, 
# в котором указаны необходимые к установке зависимости.

COPY requirements.txt requirements.txt

# Создает новый слой и , в данном случае, устанавливает необходимые зависимости.

RUN pip3 install -r requirements.txt

# Копируем файлы и папки.

COPY . .

# Команда, которая выполняется при запуске контейнера.

CMD ["python3", "-m" , "flask", "run", "--host=0.0.0.0"]
***


sudo docker build -t python-docker .

It's done!!

```



