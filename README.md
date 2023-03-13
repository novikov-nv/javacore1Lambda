# javacore1Lambda
## Задача 1: Калькулятор
Описание
Создайте класс Calculator. В нем создайте статическую переменную типа Supplier. Это функциональный интерфейс, реализующий метод get().
С помощью данной переменной можно будет получить экземпляр класса Calculator. Реализуйте ссылку на вызов конструктора класса Calculator() { }.

static Supplier<Calculator> instance = Calculator::new;
Далее добавьте несколько переменных типа BinaryOperator для математических операций над двумя числами. Типизируйте их как Integer:

BinaryOperator<Integer> plus = (x, y) -> x + y;
BinaryOperator<Integer> minus = (x, y) -> x - y;
BinaryOperator<Integer> multiply = (x, y) -> x * y;
BinaryOperator<Integer> devide = (x, y) -> x / y;
Добавьте несколько переменных типа UnaryOperator для произведения математических операций над одним числом:

UnaryOperator<Integer> pow = x -> x * x;
UnaryOperator<Integer> abs = x -> x > 0 ? x : x * -1;
Добавьте переменную типа Predicate для определения положительное ли число:

Predicate<Integer> isPositive = x -> x > 0;
Добавьте переменную типа Consumer для вывода числа в консоль. Используйте для этого ссылку на статический метод println():

Consumer<Integer> println = System.out::println;
Реализация
В классе Main в методе main() создайте экземпляр класса Calculator через вызов статической переменной instance:

Calculator calc = Calculator.instance.get();
Произведите несколько математических операций над числами:

int a = calc.plus.apply(1, 2);
int b = calc.minus.apply(1,1);
int c = calc.devide.apply(a, b);
И выведите в консоль результат:

calc.println.accept(c);
Обратите внимание на то, что приведенный выше код работать не будет. 
С помощью комментария в коде объясните причину возникновения ошибки, в чем заключается ошибка и способы ее решения. 
(Подсказка: обратите внимание на реализацию тернарного оператора в переменной abs.
Для решения проблемы можете реализовать аналог, либо сделать полноценный многострочный блок кода с { return }).

## Задача 2: Работяга
Описание
В данной задаче вам необходимо реализовать класс Worker, который будет выполнять некоторые задачи и возвращать результат в родительский класс Main.

public class Worker {

}
Для того, чтобы класс Worker мог вернуть результат своей работы, реализуйте собственный функциональный интерфейс OnTaskDoneListener. В нем определите только один метод onDone() без реализации и пометьте интерфейс аннотацией @FunctionalInterface:

@FunctionalInterface
public interface OnTaskDoneListener {
    void onDone(String result);
}
Добавьте в класс Worker переменную callback типа OnTaskDoneListener:

private OnTaskDoneListener callback;
Передайте в класс Worker ее значение через конструктор:

public Worker(OnTaskDoneListener callback) {
    this.callback = callback;
}
Смоделируйте выполнение классом Worker какой либо работы, например:

public void start() {
    for (int i = 0; i < 100; i++) {
        callback.onDone("Task " + i + " is done");
    }
}
Обратите внимание на то, что каждая итерация цикла означает выполнение задачи, результат который передается через метод onDone() функционального интерфейса OnTaskDoneListener.

Реализация
В классе Main в методе main() определите переменную listener типа OnTaskDoneListener через лямбда-выражение:

OnTaskDoneListener listener = System.out::println;
Далее создайте экземпляр класса Worker и передайте в конструктор класса listener:

Worker worker = new Worker(listener);
worker.start();
Обратите внимание на консоль. Все предполагаемые 100 задач были выполнены успешно.

Однако может случиться так, что выполнение одной из задач может закончиться неуспешно. Смоделируйте ситуацию, в которой 33 задача закончится неуспешно, и выведите информацию об этом в класс Main. Для этого создайте новый функциональный интерфейс OnTaskErrorListener, определите там метод onError(). Добавьте в класс Worker переменную errorCallback типа OnTaskErrorListener. Значение переменной передавайте так же через конструктор. Таким образом, в консоле после выполнения вашего кода все задачи, кроме 33, должны закончиться успешно, а 33 - оповестит об ошибке. 
