# Прогнозирование температуры звезды

## Цель проекта
Разработать нейронную сеть для предсказания абсолютной температуры на поверхности обнаруженных звезд.

## Используемые библиотеки
Для запуска проекта необходимо установить следующие библиотеки:
- matplotlib
- numpy
- optuna
- pandas
- seaborn
- sklearn
- skorch
- torch

## Что было сделано
- проанализировала исходный датасет и выполнила предобработку данных: при проверке на уникальные значения столбца с цветом звезды выявила некорректно записанные значения (пробелы, дефисы в названии и разный регистр), а также цвета с малым количеством значений (1-3 звезды). Такие строки я удалила и оставила в датасете 5 основых цветов звезд - это важно для обобщающей способности модели;
- в ходе исследовательского анализа изучила характеристики звезд и их зависимости - разобралась с природой распределения данных и обработала аномальные значения;
- разделила данные на обучающую и тестовую выборки, отмасштабировала количественные признаки и закодировала категориальные признаки;
- следующим этапом я построила базовую модель нейронной сети, создала класс и задала архитектуру нейронной сети - подобрала количество скрытых слоев и количество нейронов на них, функции активации на скрытых и выходных слоях. Инициализоровала веса равномерным распределением, в качестве оптимизатора параметров взяла Adam, число эпох обучения подобрала с помощью EarlyStopping. В качестве ключевой метрики использовала квадратный корень из среднеквадратичной ошибки. RMSE базовой модели на обучающей выборке равно 4011.08, на тестовой - 4949.99;
- для улучшения базовой модели реализовала перебор параметров нейросети: dropout, batch_size, learning_rate и patience. Для перебора параметров использовала optuna. Удалось достичь значения метрики RMSE улучшенной модели на тестовой выборке: 4371.22.

## Итоговые результаты
Были обучены две модели нейронной сети: базовая и с улучшением. Архитектура нейронной сети:
- нейронная сеть полносвязная;
- на входном слое 12 нейронов:
- на выходном слое 1 нейрон, так как целевая переменная представлена в количественной шкале и решается задача регрессии;
- количество скрытых слоев - 6 и с количеством нейронов на них 18, 20, 15, 10, 8, 4 соответственно;
- на входном и скрытых слоях - функция активации ReLU;
- веса инициализированы равномерным распределением;
- функция потерь - среднее абсолютное отклонение L1Loss.

Метрика RMSE у базовой модели на обучающей выборке - 4011.08, на тестовой - 4949.99.

С помощью optuna подобрала наилучшие параметры:
- dropout - 0.1;
- learning_rate - 0.004949503297973507;
- batch_size - 15;
- patience - 200.

Удалось достичь RMSE на тестовой выборке 4371.22.

Дополнительно строила графики лосс-функции, чтобы наблюдать результат обучения модели. В обоих случаях значения функции потерь уменьшались и в конце обучения близились к нулю. А также вывела графики прогноза температуры звезды и фактического значения для наглядной визуализации результатов.

