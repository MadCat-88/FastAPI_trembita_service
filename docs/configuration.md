## Встановлення за допомогою скрипта deploy.sh

## Опис 

Для автоматизації процесу встановлення та подальшої роботи вебсервісу було створено скрипт `deploy.sh`.
**Даний скрипт:**

1. Встановлює системні залежності.
2. Клонує репозиторій.
3. Створює та активує віртуальне середовище.
4. Встановлює залежності Python.
5. Встановлює СУБД MariaDB
5. Налаштовує конфігурацію бази даних.
6. Створює структуру бази даних за допомогою Alembic.
7. Створює систему управління службами systemd для запуску вебсервісу.

**Для того, щоб встановити даний вебсервіс за допомогою скрипта необхідно:**

1. Завантажити скрипт:
```bash
wget https://raw.githubusercontent.com/kshypachov/FastAPI_trembita_service/master/deploy.sh
```
2. Відредагуйте скрипт deploy.sh, замінивши значення змінних DB_USER, DB_PASSWORD, DB_NAME, DB_HOST та DB_PORT на ваші реальні дані.
3. Зробити файл виконуваним:

```bash
chmod +x deploy.sh
```

4. Запустити скрипт:
```bash
./deploy.sh
```

### Керування сервісом
- Запустити сервіс: 
```bash
sudo systemctl start fastapi_trembita_service
```

- Зупинити сервіс:
```bash
sudo systemctl stop fastapi_trembita_service
```

- Конфігурація сервісу зберігається у файлі `config.ini` :
- Опис полів `config.ini` :

   ```ini
   [database]
   # Тип бази даних, яку ви використовуєте. Можливі значення: mysql або postgres
   db_type = mysql
   
   # IP-адреса або доменне ім'я сервера бази даних
   host = your_db_host
   
   # Порт, через який здійснюється підключення до бази даних. За замовчуванням для MySQL це 3306
   port = your_db_port
   
   # Ім'я бази даних, до якої потрібно підключитися
   name = your_db_name
   
   # Ім'я користувача для підключення до бази даних
   username = your_db_user
   
   # Пароль користувача для підключення до бази даних
   password = your_db_password
   
   [logging]
   # Шлях до файлу, куди буде записуватися лог
   filename = path/to/client.log
   
   # filemode визначає режим, в якому буде відкритий файл логування.
   # 'a' - дописувати до існуючого файлу
   # 'w' - перезаписувати файл кожен раз при старті програми
   filemode = a
   
   # format визначає формат повідомлень логування.
   # %(asctime)s - час створення запису
   # %(name)s - ім'я логгера
   # %(levelname)s - рівень логування
   # %(message)s - текст повідомлення
   # %(pathname)s - шлях до файлу, звідки було зроблено виклик
   # %(lineno)d - номер рядка у файлі, звідки було зроблено виклик
   format = %(asctime)s,%(msecs)d %(name)s %(levelname)s %(message)s
   
   # dateformat визначає формат дати в повідомленнях логування.
   # Можливі формати можуть бути такими, як:
   # %Y-%m-%d %H:%M:%S - 2023-06-25 14:45:00
   # %d-%m-%Y %H:%M:%S - 25-06-2023 14:45:00
   dateformat = %H:%M:%S
   
   # level визначає рівень логування. Найбільш детальний це DEBUG, за замовчуванням INFO
   # DEBUG - докладна інформація, корисна для відлагодження роботи, логується вміст запитів та відповідей
   # INFO - загальна інформація про стан виконання програми
   # WARNING - попередження про можливі проблеми
   # ERROR - помилки, які завадили нормальному виконанню
   # CRITICAL - критичні помилки, що призводять до завершення програми
   level = DEBUG
   ```

### Завершення
Сервіс запущено! Після запуску сервера ви можете отримати доступ до автоматичної документації API за наступними адресами:

- Swagger UI: http://[адреса серверу]:8000/docs
- ReDoc: http://[адреса серверу]:8000/redoc