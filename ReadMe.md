Петров В.А.

Домашнее задание по дисциплине "Параллельное программирование" в Computer science center.
В задании требовалось написать свою реализацию FixedThreadPool. Запрещено использовать какие-либо встроенные и сторонние библиотеки для создания пула / конкуррентных контейнеров.

# Комментарии к коду
* Многие `synchronize` блоки можно безболезненно убрать, если использовать конкуррентные структуры. Они стоят не для защиты от ломания алгоритма, а для защиты от выброса случайного `exception` при модификации этих структур через множество итераторов из разных потоков одновременно.

# Документация
#### **FixedThreadPool**
* *submit(Task task)*.
* *stop()* - просит все потоки завершить свою работу.

#### **InterruptionMonitor**
Интерфейс. Позволяет отслеживать состояние процесса выполнения задачи (после его запуска).

* *isInterrupted()*. Возвращает true, если задачу просят прерваться. Предполагается, что составитель задачи будет использовать этот метод аналогично Thread.isInterrupted() внутри Task.run().

#### **Task**
Интерфейс задачи.
 
* *run()*
* *getResult()*
* *setInterruptionMonitor(InterruptionMonitor monitor)* - задаёт монитор для данной задачи.
    
## Вспомогательные классы
#### **AbstractTask**
Пустой класс, реализующий интерфейс Task. Удобен для унаследования в тестовых задачах.

# как пользоваться CLI
поддерживаемые команды:  
add sleeping 1000  
add counting  
add throwing  
add recursive  
Добавляют задачи заданного типа в очередь. У sleeping дополнительный аргумент - длительность задачи.  
После добавления задачи в консоли будет показан её номер.  

cancel 5
отмена задачи с номером 5

result 5
показывает результат работы задачи

iscanceled 5
показывает, отменена ли задача

exception 5
показывает, какое исключение было выброшено в процессе работы задачи.