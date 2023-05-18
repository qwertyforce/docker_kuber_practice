# Базовый image
FROM python:3.10-alpine

# Переменные, используемые для создания окружения, в котором запустится приложение
ARG USER=app 
ARG UID=1001
ARG GID=1001

# Создание пользователя операционной системы и его домашнего каталога
RUN addgroup -g ${GID} -S ${USER} \
   && adduser -u ${UID} -S ${USER} -G ${USER} \
   && mkdir -p /app \
   && chown -R ${USER}:${USER} /app
USER ${USER}

# Переход в каталог /app
WORKDIR /app


# Копирование файла в домашний каталог
COPY --chown=$USER:$USER hello.html /app

# Публикация порта, который прослушивается приложением
EXPOSE 8000

# Команда запуска приложения
CMD ["python3", "-m", "http.server", "8000"]