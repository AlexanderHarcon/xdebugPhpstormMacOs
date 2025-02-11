Встановлення та налаштування Xdebug на macOS
1. Встановлення Xdebug
   1. Відкрийте термінал.
   2. Виконайте команду для встановлення Xdebug через pecl: pecl install xdebug
2. Налаштування Xdebug
   1. Після встановлення, знайдіть конфігураційний файл Xdebug. Зазвичай він знаходиться в /opt/homebrew/etc/php/8.3/conf.d/99-xdebug.ini.
   2. Відкрийте конфігураційний файл для редагування: nano /opt/homebrew/etc/php/8.3/conf.d/99-xdebug.ini
   3. Додайте або змініть наступні налаштування:
      ```
      zend_extension="xdebug.so"
      xdebug.mode=debug
      xdebug.start_with_request=yes
      xdebug.client_host=127.0.0.1
      xdebug.client_port=9003
      ```
   4. Збережіть файл і перезапустіть веб-сервер, якщо він працює.
3. Налаштування PHPStorm
   1. Відкрийте PHPStorm.
   2. Перейдіть до Preferences або Settings (Cmd + , на macOS).
   3. Перейдіть до Languages & Frameworks -> PHP -> Debug.
       *Переконайтеся, що порт налагодження встановлений на 9003.
   4. Перейдіть до Languages & Frameworks -> PHP -> Servers.
       *Додайте новий сервер:
       Name: localhost
       Host: localhost
       Port: 8080
       Debugger: Xdebug
     *Увімкніть Use path mappings і встановіть відповідності шляхів:
       Server Path: /Users/tensei/../../I stage
       Local Path: /path/to/your/project
   5. Натисніть OK для збереження налаштувань.
   6. Налаштування налагодження:
      1. Перейдіть до Run -> Edit Configurations.
      2. Натисніть + і виберіть PHP Remote Debug.
          Name: Вкажіть ім'я конфігурації, наприклад, Localhost Debug.
          Server: Виберіть сервер, який ви налаштували раніше (localhost).
          IDE Key: Введіть PHPSTORM (або значення, яке ви вказали в конфігурації Xdebug).
          Поставте галочку Filter debug connection by IDE key.
   7. Увімкніть прослуховування налагоджувальних з'єднань в PHPStorm (значок телефону у верхньому правому куті).
4. Запуск локального сервера
   1. Відкрийте термінал.
   2. Запустіть сервер: php -S localhost:8080
5. Використання Xdebug
   1. Додайте точку зупинки (breakpoint) у вашому коді в PHPStorm.
   2. Відкрийте ваш браузер і зробіть запит до вашого скрипту, наприклад, http://localhost:8080/test.php.

FAQ по помилкам
1. Помилка: Remote file path is not mapped to any file path in project
   Рішення:
Відкрийте Preferences або Settings -> Languages & Frameworks -> PHP -> Servers.
Переконайтеся, що встановлені правильні відповідності шляхів.
2. Помилка: Failed loading Zend extension 'xdebug'
   Рішення:
Переконайтеся, що в конфігураційному файлі Xdebug (/opt/homebrew/etc/php/8.3/conf.d/99-xdebug.ini) правильний шлях до xdebug.so.
3. Помилка: Could not connect to debugging client
   Рішення:
Переконайтеся, що PHPStorm прослуховує налагоджувальні з'єднання.
Переконайтеся, що налаштування xdebug.client_host та xdebug.client_port правильні.
Переконайтеся, що порт 9003 не зайнятий іншими процесами.
4. Перевірка зайнятості порту на macOS
   Команда: lsof -i :9003
5. Помилка: discover client host: is OFF
   Рішення:
Відкрийте файл конфігурації Xdebug. Наприклад, ви можете використовувати nano з терміналу: sudo nano /opt/homebrew/etc/php/8.3/conf.d/99-xdebug.ini
Додайте або змініть рядок у конфігураційному файлі, щоб увімкнути xdebug.discover_client_host: xdebug.discover_client_host = 1
Збережіть файл і вийдіть з редактора (Control + O, потім Enter для збереження і Control + X для виходу в nano).
6. Перевірка налаштувань відлагоджувача на веб-сервері
   1. Створіть тестовий файл info.php з наступним вмістом: <?php phpinfo(); 
   2. Завантажте info.php у кореневу директорію вашого веб-сервера.
   3. Відкрийте URL, де знаходиться ваш файл, наприклад, http://localhost/info.php.
   4. Знайдіть розділ Xdebug у виведенні phpinfo().
   5. Перевірте важливі налаштування
      xdebug.remote_enable = On
      xdebug.client_host = 127.0.0.1 (або інший відповідний IP)
      xdebug.client_port = 9003
   6. Скопіюйте всю сторінку info.php та вставте за адресою:
      PhpStorm -> Settings(cmd + ,) -> Debug -> Validate(У відкритому вікні вставте скопійований текс в розділ Output phpinfo())-> Validate 



Корисні команди для терміналу
   ** php -i | grep xdebug
