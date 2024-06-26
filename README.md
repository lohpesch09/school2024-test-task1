# Тестовое задание для отбора на Летнюю ИТ-школу КРОК по разработке

## Условие задания
Один развивающийся и перспективный маркетплейс активно растет в настоящее время. Текущая команда разработки вовсю занята тем, что развивает ядро системы. Помимо этого, перед CTO маркетплейса стоит задача — разработать подсистему аналитики, которая на основе накопленных данных формировала бы разнообразные отчеты и статистику.

Вы — компания подрядчик, с которой маркетплейс заключил рамочный договор на выполнение работ по разработке этой подсистемы. В рамках первого этапа вы условились провести работы по прототипированию и определению целевого технологического стека и общих подходов к разработке.

На одном из совещаний с Заказчиком вы определили задачу, на которой будете выполнять работы по прототипированию. В качестве такой задачи была выбрана разработка отчета о периодах наибольших трат со стороны пользователей.

Аналитики со стороны маркетплейса предоставили небольшой срез массива данных (файл format.json) о покупках пользователей, на примере которого вы смогли бы ознакомиться с форматом входных данных. Каждая запись данного среза содержит следующую информацию:
- Идентификатор пользователя;
- Дата и время оформления заказа;
- Статус заказа;
- Сумма заказа.

В пояснительной записке к массиву данных была уточняющая информация относительно статусов заказов:
- COMPLETED (Завершенный заказ);
- CANCELED (Отмененный заказ);
- CREATED (Созданный заказ, еще не оплаченный);
- DELIVERY (Созданный и оплаченный заказ, который доставляется).

Необходимо разработать отчет, вычисляющий по полученному массиву данных месяц, когда пользователи тратили больше всего. Если максимальная сумма пользовательских трат была в более, чем одном месяце, отчет должен показывать все такие месяцы. В отчете должны учитываться только завершенные заказы.

Требования к реализации:
1. Реализация должна содержать, как минимум, одну процедуру (функцию/метод), отвечающую за формирование отчета, и должна быть описана в readme.md в соответствии с чек-листом;
2. В качестве входных данных программа использует json-файл (input.json), соответствующий структуре, описанной в условиях задания;
3. Процедура (функция/метод) формирования отчета должна возвращать строку в формате json следующего формата:
   - {«months»: [«march»]} 
   - {«months»: [«march», «december»]}
4. Найденный в соответствии с условием задачи месяц должен выводиться на английском языке в нижнем регистре. Если месяцев несколько, то на вывод они все подаются на английском языке в нижнем регистре в порядке их следования в течение года.

## Автор решения
Макаров Алексей Евгеньевич
## Описание реализации

В начале метода main создаётся переменная jsonArray класса JSONArray, которой присваивается значение, возвращаемое функцией readJsonFile. В функцию readJsonFile в качестве аргумента передаётся в формате String название файла, который нужно считать, а сама реализация метода состоит из блоков try и cath, где, если получается считать файл, функция записывает его содержимое в переменную типа JSONArray и возвращает её значение.

Когда в основном методе main мы записали в переменную jsonArray значение, которое вернула функция readJsonFile, мы передаём jsonArray в качестве параметра в функцию generateReport. Идея функции generateReport состоит в следующем: заводим переменную типа JSONObject, куда будем записывать ArrayList под названием monthArrayWithMaxSum по ключу "month", а также переменную maxSumOfSpentMoney, с которой каждый раз будет сравниваться значение суммарной потраченной клиентами суммы за месяц. Создаём цикл, который пробегает все порядковые номера месяцев от 1 до 12, и внутри него заводим переменную sumOfSpentMoneyInMonth, котороя будет будет обновляться каждую итерацию за счёт того, что каждый раз ей присваивается значение, возвращаемое функцией getSumOfSpentMoneyInMonth (Функцию getSumOfSpentMoneyInMonth я опишу подробно в следующем абзаце). Затем следуют условные операторы, первый из которых проверяет, если обновившееся значение sumOfSpentMoneyInMonth стало больше maxSumOfSpentMoney. Если это так, то monthArrayWithMaxSum очистится от старых элементов, и в него запишется текущий месяц. Второй условный оператор проверяет, если sumOfSpentMoneyInMonth равно значению maxSumOfSpentMoney. Если это так, то в monthArrayWithMaxSum добавится текущий месяц. По завершении всех 12-и итераций в переменную jsonObjectMonths типа JSONObject по ключу "month" запишется monthArrayWithMaxSum. После этого функция выведет на консоль jsonObjectMonths и в квадратных скобках можно будет увидеть список месяцев с наибольшими тратами на заказы. Функция generateReport возвращает jsonObjectMonths.toJSONString() - строку в формате json.

В метод getSumOfSpentMoneyInMonth в качетве параметра передаётся счётчик monthNumber из цикла месяцев функции generateReport, а также jsonArray, который передавался в качестве параметра в функцию generateReport. Далее заводим переменную sumOfSpentMoneyInMonth, которй присваиваем вначале значение 0. Затем идёт цикл, который пробегает все объекты в jsonArray.Далле следует условный оператор, который проверяет, если у текущего объекта месяц, в котором совершён заказ, совпадает с переданным в функцию monthNumber, а также если статус заказа является "Completed". Если оба условия выполнены, то тогда из объекта по ключу "total" извлекается сумма, потраченная на текущий заказ, и прибавляется в переменную sumOfSpentMoneyInMonth. По завершении работы функция вернёт значение sumOfSpentMoneyInMonth.


## Инструкция по сборке и запуску решения

1) Скачайте с официального сайта maven-сборщик.
2) Пропишите в командной строке команду, которая позволит скопировать репозиторий: git clone https://github.com/lohpesch09/school2024-test-task1
3) Перейдите в директорию, куда был скопирован репозиторий и пропишите команду, которая позволит собрать проект: mvn clean package
4) В этой же директории пропишите команду, которая выполнит приложение, предварительно убедившись, что в собранном проекте присутствует файл input.json: mvn exec:java


