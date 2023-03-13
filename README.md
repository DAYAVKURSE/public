# SQL_DB_Loader
Mini-framework for working with a local sql database and updating its contents from Google sheets

  The code is a Python script that imports several modules, defines a custom exception class, and two classes: Database and DBUpdater. The Database class has methods for reading and writing data to an SQLite database, while the DBUpdater class has a method for copying data from a Google Sheets spreadsheet to the SQLite database using the Database class.
  The code starts by importing the sqlite3, functools, datetime, gspread, and inspect modules. It then defines a custom exception class called DBError that takes three arguments: message, error_code, and input. The init method initializes these arguments and creates a technical_data attribute that combines them into a string. The error_code, input, and message methods return their respective attributes, while the str method returns the technical_data attribute.
  The ensure_connection decorator function is defined next. This function takes a function as an argument and returns a new function that wraps the original function. The wrapper function opens a connection to the SQLite database using the connect method of the Database class and passes it to the original function along with any arguments and keyword arguments.
  The Database class is defined next. Its init method takes a db_name argument and initializes the db_name attribute. The connect method takes an optional error_code argument and attempts to connect to the SQLite database using the sqlite3.connect method. If an error occurs, it raises a DBError exception with the error message, error code, and input arguments.
The read method takes four arguments: conn, table_name, out, and params. It uses the cursor method of the connection object to execute a SELECT query on the specified table and columns. If params are provided, it adds a WHERE clause to the query to filter the results. It then fetches all the rows returned by the query and returns them as a list. If no rows are returned, it returns an empty list. If an error occurs, it raises a DBError exception with the error message, error code, and input arguments.
  The write method takes three arguments: conn, query, and params. It uses the cursor method of the connection object to execute the specified SQL query with the given parameters. If an error occurs, it raises a DBError exception with the error message, error code, and input arguments.
The DBUpdater class is defined next. Its init method takes a db argument and initializes the db attribute. It also creates a gspread_client attribute using the gspread.service_account method and passing it a filename argument.
  The copy_table method takes three arguments: sheet_name, table_name, and column_names. It uses the worksheet method of the gspread_client object to get a worksheet with the specified name. It then uses the get_all_records method of the worksheet object to get all the rows in the worksheet as a list of dictionaries. It then iterates over each column in the worksheet and updates or inserts the corresponding row in the SQLite database using the read and write methods of the Database class. If an error occurs, it raises a DBError exception with the error message, error code, and input arguments.
  The run_update method takes a sheet_list argument, which is a dictionary of sheet names, table names, and column names. It iterates over each sheet in the sheet_list and calls the copy_table method with the appropriate arguments. It then prints a message indicating that the data has been copied to the SQLite database.

Мини-фреймворк для работы с локальной sql базой данных и обновлением ее содержимого из Гугл таблиц

  Код представляет собой сценарий Python, который импортирует несколько модулей, определяет собственный класс исключений и два класса: Database и DBUpdater. Класс Database имеет методы для чтения и записи данных в базу данных SQLite, а класс DBUpdater имеет метод для копирования данных из электронной таблицы Google Sheets в базу данных SQLite с использованием класса Database.
  Код начинается с импорта модулей sqlite3, functools, datetime, gspread и inspect. Затем он определяет собственный класс исключений с именем DBError, который принимает три аргумента: сообщение, код_ошибки и ввод. Метод init инициализирует эти аргументы и создает атрибут Technical_Data, который объединяет их в строку. Методы error_code, input и message возвращают соответствующие атрибуты, а метод str возвращает атрибут Technical_Data.
  Затем определяется функция декоратора sure_connection. Эта функция принимает функцию в качестве аргумента и возвращает новую функцию, являющуюся оболочкой исходной функции. Функция-оболочка открывает соединение с базой данных SQLite с помощью метода connect класса Database и передает его исходной функции вместе с любыми аргументами и аргументами ключевого слова.
  Далее определяется класс базы данных. Его метод init принимает аргумент db_name и инициализирует атрибут db_name. Метод connect принимает необязательный аргумент error_code и пытается подключиться к базе данных SQLite, используя метод sqlite3.connect. При возникновении ошибки возникает исключение DBError с сообщением об ошибке, кодом ошибки и входными аргументами.
  Метод чтения принимает четыре аргумента: conn, table_name, out и params. Он использует метод курсора объекта подключения для выполнения запроса SELECT к указанной таблице и столбцам. Если указаны параметры, он добавляет в запрос предложение WHERE для фильтрации результатов. Затем он извлекает все строки, возвращенные запросом, и возвращает их в виде списка. Если строки не возвращаются, возвращается пустой список. При возникновении ошибки возникает исключение DBError с сообщением об ошибке, кодом ошибки и входными аргументами.

  Метод записи принимает три аргумента: conn, query и params. Он использует метод курсора объекта подключения для выполнения указанного SQL-запроса с заданными параметрами. При возникновении ошибки возникает исключение DBError с сообщением об ошибке, кодом ошибки и входными аргументами.
  Метод copy_table принимает три аргумента: имя_листа, имя_таблицы и имена_столбцов. Он использует метод рабочего листа объекта gspread_client для получения рабочего листа с указанным именем. Затем он использует метод get_all_records объекта рабочего листа, чтобы получить все строки рабочего листа в виде списка словарей. Затем он перебирает каждый столбец на листе и обновляет или вставляет соответствующую строку в базу данных SQLite, используя методы чтения и записи класса Database. При возникновении ошибки возникает исключение DBError с сообщением об ошибке, кодом ошибки и входными аргументами.
  Метод run_update принимает аргумент sheet_list, который представляет собой словарь имен листов, имен таблиц и имен столбцов. Он выполняет итерацию по каждому листу в sheet_list и вызывает метод copy_table с соответствующими аргументами. Затем он печатает сообщение о том, что данные были скопированы в базу данных SQLite.
