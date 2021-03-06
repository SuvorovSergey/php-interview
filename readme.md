
# Вопросы с собеседований на PHP разработчика

## Содержание
* ### [Junior](#junior-1)
    * [Назовите простые типы данных, поддерживаемые в РНР](#назовите-простые-типы-данных-поддерживаемые-в-рнр)
    * [Что такое ссылки?](#что-такое-ссылки)
    * [Каковы основные операции с использованием ссылок?](#каковы-основные-операции-с-использованием-ссылок)
    * [Что такое инкремент и декремент, в чем разница между префиксным и постфиксным инкрементом и декрементом?](#что-такое-инкремент-и-декремент-в-чем-разница-между-префиксным-и-постфиксным-инкрементом-и-декрементом)
    * [Что такое рекурсия?](#что-такое-рекурсия)
    * [Что такое чистая функция?](#что-такое-чистая-функция)
    * [Что такое функции первого порядка?](#что-такое-функции-первого-порядка)
    * [Что такое иммутабельность?](#что-такое-иммутабельность)
    * [В чем разница между =, == и ===?](#в-чем-разница-между---и-)
    * [Какие знаете принципы ООП?](#какие-знаете-принципы-ооп)
    * [Чем отличаются ключевые слова: include и require?](#чем-отличаются-ключевые-слова-include-и-require)
    * [Какие модификаторы видимости есть в РНР?](#какие-модификаторы-видимости-есть-в-рнр)
    * [Что такое интерфейсы?](#что-такое-интерфейсы)
    * [Зачем нужны интерфейсы?](#зачем-нужны-интерфейсы)
    * [Что такое абстрактный класс и чем он отличается от интерфейса?](#что-такое-абстрактный-класс-и-чем-он-отличается-от-интерфейса)
    * [Какие магические методы вы знаете и как их применяют?](#может-ли-абстрактный-класс-содержать-частный-метод)
    * [Что такое генераторы и как их использовать?](#что-такое-генераторы-и-как-их-использовать)
    * [Что такое traits? Альтернативное решение? Приведите пример.](#что-такое-traits-альтернативное-решение-приведите-пример)
    * [Опишите поведение при использовании traits с одинаковыми именами полей или методов.](#опишите-поведение-при-использовании-traits-с-одинаковыми-именами-полей-или-методов)
    * [Будут ли доступны частные методы trait в классе?](#будут-ли-доступны-частные-методы-trait-в-классе)
    * [Можно ли компоновать traits в trait?](#можно-ли-компоновать-traits-в-trait)
* ### [Middle](#middle-1)
* ### [Senior](#senior-1)


## Junior

## Назовите простые типы данных, поддерживаемые в РНР

Четыре скалярных типа:

```text  
bool  
int  
float  
string  
```  

Четыре смешанных типа:

```text  
array  
object  
callable (Callback-функции могут быть обозначены объявлением типа callable)  
iterable (псевдотип, введённый в PHP 7.1. Он принимает любой массив (array) или объект, реализующий интерфейс Traversable. Оба этих типа итерируются с помощью foreach и могут быть использованы с yield from в генераторах.)  
```  

И два специальных типа:

```text  
resource  
NULL  
```  

**[⬆ вернуться к началу](#содержание)**


## Что такое ссылки?
Ссылки в PHP - это средство доступа к содержимому одной переменной под разными именами. Они не похожи на указатели C; например, вы не можете выполнять над ними адресную арифметику, они не являются реальными адресами в памяти и т.д. Для получения дополнительной информации смотрите Чем ссылки не являются. Вместо этого указатели в PHP - это псевдонимы в таблице имён переменных. В PHP имя переменной и её содержимое - это разные вещи, поэтому одно содержимое может иметь разные имена. Можно провести аналогию с именами файлов и файлами в Unix: имена переменных - записи в каталоге, а содержимое переменной - это сам файл. Ссылки в PHP - аналог жёстких ссылок в файловых системах Unix.

**[⬆ вернуться к началу](#содержание)**


## Каковы основные операции с использованием ссылок?

Есть три основных операции с использованием ссылок: присвоение по ссылке, передача по ссылке и возврат по ссылке.

* Ссылки PHP позволяют создать две переменные указывающие на одно и то же значение.
```php  
$a = &$b;  
```  
> $a и $b здесь абсолютно эквивалентны, но это не означает, что $a указывает на $b или наоборот. Это означает, что $a и $b указывают на одно и то же значение.

* Передача параметров по ссылке. При этом локальная переменная в функции и переменная в вызывающей области видимости ссылаются на одно и то же содержимое.

```php  
function foo(&$var) {  
    $var++;
}

$a = 5; foo($a);  
```  
> Этот код присвоит $a значение 6.

* Возврат по ссылке используется в тех случаях, когда вы хотите использовать функцию для выбора переменной, с которой должна быть связана данная ссылка.

```php  
class foo {  
    public $value = 42;  
  
    public function &getValue() {  
        return $this->value;  
    }  
}  

$obj = new foo;  
$myValue = &$obj->getValue(); // $myValue указывает на $obj->value, равное 42.  
$obj->value = 2;  
echo $myValue;                // отобразит новое значение $obj->value, то есть 2.  
```

**[⬆ вернуться к началу](#содержание)**



## Что такое инкремент и декремент, в чем разница между префиксным и постфиксным инкрементом и декрементом?

Это унарные операции, они увеличивают или уменьшают на единицу число, записанное в переменную и возвращают переменную.  
При использовании префиксной нотации сначала происходит изменение переменной, а потом возврат.  
При использовании постфиксной нотации — наоборот: сначала возврат, а потом изменение переменной.  

```php  
$x = 5;  
  
echo ++$x; // => 6  
echo $x;   // => 6  
  
echo $x++; // => 6  
echo $x;   // => 7  
```

**[⬆ вернуться к началу](#содержание)**

## Что такое рекурсия?
В применении к программированию это значит написание такого алгоритма функции, в котором функция будет вызывать сама себя.

В более сложном случае функция может вызывать другую функцию, которая будет вызывать исходную функцию.

Используя рекурсию, нужно понимать её опасность: ресурсы компьютера не безграничны, и если глубина рекурсии будет достаточно большой (или вообще бесконечной), то это приведет к переполнению стека.

```php  
// функция будет бесконечно вызывать саму себя  
function foo() {  
    return foo();
}  
  
foo();  
```

Пример вычисления факториала с использованием рекурсии

```php  
function factorial($n) {  
    if ($n <= 1) { 
        return 1; 
    }
        
    return $n * factorial($n - 1); 
}
   
echo factorial(5); // 120   
```

**[⬆ вернуться к началу](#содержание)**

## Что такое чистая функция?
Чистая функция — это такая функция которая зависит только от своих аргументов, всегда возвращает одинаковый результат для одних и тех же аргументов и не имеет побочных эффектов (не меняет значения переменных за пределами себя).

```php  
date('Y'); // функция не является чистой, так как возвращаемое значение будет другим в следующем году  
rand(); // еще один пример функции, не являющейся чистой  
mkdir('dirname'); // функция не является чистой, так как возвращаемые значения могут быть разными (true/false)  
max([3, 5, 8]); // чистая функция  
```  
**[⬆ вернуться к началу](#содержание)**


## Что такое функции первого порядка?
Это такие функции, которые могут принимать другие функции, как аргументы, или возвращать функцию.
```php  
function higherOrderFunction(callable $func) {  
    $func();
}  
```  

array_filter функция высшего порядка

```php  
$arrayOfNums = [1,2,3,4,5];  
  
function isEven($num) {  
    return ($num % 2) === 0;
}  
  
$evenNums = array_filter($arrayOfNums, 'isEven');  
  
var_dump($evenNums); // Выводит массив четных чисел [2, 4]  
```

**[⬆ вернуться к началу](#содержание)**

## Что такое иммутабельность?
Иммутабельность это неизменяемость. В применении к объектам можно сказать, что объект иммутабельный, если его состояние нельзя изменить после создания.

**[⬆ вернуться к началу](#содержание)**

## В чем разница между =, == и ===?
= это оператор присваивания. Означает, что левый операнд получает значение правого выражения.

Результатом выполнения оператора присваивания является само присвоенное значение. Это позволяет делать трюки наподобие:

```php  
$a = ($b = 4) + 5; // $a теперь равно 9, а $b было присвоено 4.  
```  

== и === это операторы сравнения.

$a == $b   Равно  true если $a равно $b после преобразования типов.

$a === $b  Тождественно равно true если $a равно $b и имеет тот же тип.

Подробнее о преобразовании типов https://www.php.net/manual/ru/language.operators.comparison.php

**[⬆ вернуться к началу](#содержание)**


## Какие знаете принципы ООП?
  Инкапсуляция, наследование, полиморфизм, абстракция.

**Инкапсуляция** — размещение в одном компоненте данных и методов, которые с ними работают. Также в языках реализующих инкапсуляцию есть механизм сокрытия, позволяющий разграничивать доступ к различным компонентам программы. В php обеспечивается модификаторами доступа.

**Наследование** — способность объекта или класса базироваться на другом объекте или классе. Это главный механизм для повторного использования кода. Объект-потомок автоматически наследует от родителя все поля и методы, может дополнять объекты новыми полями и заменять (перекрывать) методы родителя или дополнять их.

**Полиморфизм** — одно из определений звучит так: Термин “полиморфизм” обозначает семейство различных механизмов, позволяющих использовать один и тот же участок программы с различными типами в различных контекстах.  
Если сказать несколько иначе, это взаимозаменяемость объектов реализующих один интерфейс. Т.е. способность одного и того же участка кода работать с разными типами.

**Абстракция** — отделение концепции от ее экземпляра.

**[⬆ вернуться к началу](#содержание)**

## Чем отличаются ключевые слова: include и require?
Оба выражения используются для помещения данных одного файла PHP в другой. Разница в том как они обрабатывают ошибку. Если возникает ошибка, то include генерирует предупреждение, но скрипт продолжит выполнение. Require генерирует фатальную ошибку и выполнение скрипта останавливается.

**[⬆ вернуться к началу](#содержание)**

## Какие модификаторы видимости есть в РНР?
**public** - свойства или методы, объявленные как public, могут быть доступны в любом месте.

**protected** - свойства или методы доступны только внутри класса, а также в дочерних классах.

**private** - доступ к private свойствам и методам имеет только класс, в котором эти свойства или методы объявлены.

Если модификатор доступа не указан, то он будет считаться как public.

**[⬆ вернуться к началу](#содержание)**


## Что такое интерфейсы?
Интерфейс нужно рассматривать как контракт. Он содержит только сигнатуры методов (без тела метода). Класс, реализующий этот контракт, обязан реализовать все методы интерфейса.

Интерфейсы объявляются так же, как и обычные классы, но с использованием ключевого слова interface вместо class. Тела методов интерфейсов должны быть пустыми.  
Все методы, объявленные в интерфейсах, должны быть общедоступными, что следует из самой природы интерфейса.

Для реализации интерфейса используется оператор implements. Класс должен реализовать все методы, описанные в интерфейсе, иначе произойдёт фатальная ошибка. При желании классы могут реализовывать более одного интерфейса, разделяя каждый интерфейс запятой.

>**Интерфейсы не могут содержать объявление статических методов**

>Абстрактный класс может реализовывать **только часть интерфейса**.

>**Интерфейсы могут быть унаследованы друг от друга**, так же как и классы, с помощью оператора extends.

>**Интерфейсы могут содержать константы.** Константы интерфейсов работают точно так же, как и константы классов. До PHP 8.1.0 они не могли быть переопределены классом или интерфейсом, который их наследует.

Пример

```php  
interface A  
{  
    public function foo();
}  
  
interface B extends A  
{  
    public function bar();
}  
  
interface C extends A, B  
{  
    public function baz();
}  
  
class D implements C  
{  
    public function foo() { }  
    public function bar() { }  
    public function baz() { }
}  
```  

Интерфейс с константами

```php  
interface A  
{  
    const B = 'Константа интерфейса';
}  
  
// Выведет: Константа интерфейса  
echo A::B;  
  
class B implements A  
{  
    const B = 'Константа класса';
}  
  
// Выведет: Константа класса  
// До PHP 8.1.0 этот код не будет работать,  
// потому что было нельзя переопределять константы.  
echo B::B;  
```  

**[⬆ вернуться к началу](#содержание)**

## Зачем нужны интерфейсы?
Интерфейс, совместно с объявлениями типов, предоставляет отличный способ проверки того, что определённый объект содержит определённый набор методов.

Интерфейсы нужны:
* Чтобы позволить разработчикам создавать объекты разных классов, которые могут использоваться взаимозаменяемо, поскольку они реализуют один и тот же интерфейс или интерфейсы. Типичный пример - несколько служб доступа к базе данных, несколько платёжных шлюзов или разных стратегий кеширования. Различные реализации могут быть заменены без каких-либо изменений в коде, который их использует.
* Чтобы разрешить функции или методу принимать и оперировать параметром, который соответствует интерфейсу, не заботясь о том, что ещё может делать объект или как он реализован. Эти интерфейсы часто называют Iterable, Cacheable, Renderable и так далее, чтобы описать их поведение.

**[⬆ вернуться к началу](#содержание)**

## Что такое абстрактный класс и чем он отличается от интерфейса?
Абстрактные классы в php реализуются добавлением ключевого слово abstract.

Абстрактный класс создается только для как элемент иерархии наследования. Это означает, что вы не можете создать объект абстрактного класса.

Дочерний класс, который наследует абстрактный класс, должен реализовывать методы, объявленные абстрактными в родительском классе.

Абстрактный класс хорош, когда есть некоторые общие черты, которые должны быть общими для всех объектов.

Свойства абстрактного класса не могут быть abstract.

| Интерфейс  | Абстрактный класс |  
| ------------- | ------------- |  
| Поддерживает множественное наследование  | Не поддерживает множественное наследование  |  
| Не содержит конструктор  | Может содержать конструктор  |  
|Содержит только объявление методов (сигнатуры методов)|Может содержать как сигнатуры методов так и их реализации|  
|Не может иметь модификаторов доступа - все методы по умолчанию публичные|Может иметь модификаторы доступа|  
|Методы не могут быть статическими|Только методы, содержащие реализацию, могут быть объявлены статическими|  

**[⬆ вернуться к началу](#содержание)**

## Может ли абстрактный класс содержать частный метод?
**Абстрактные методы** должны иметь модификаторы либо public, либо protected. Язык не запрещает **абстрактному классу** содержать private методы, но в дочерних классах они будут недоступны.

**[⬆ вернуться к началу](#содержание)**

## Какие магические методы вы знаете и как их применяют?
Магические методы - это специальные методы, которые переопределяют действие PHP по умолчанию, когда над объектом выполняются определённые действия.  
Магические методы вызываются автоматически. Лучший пример это метод __construct(), вызываемый автоматически при создании объекта.

Список магических методов

* __construct() конструктор, вызывается при создании экземпляра объекта
* __destruct() деструктор, вызывается при уничтожении объекта
* __call() запускается при вызове недоступных методов в контексте объекта
* __callStatic() запускается при вызове недоступных методов в статическом контексте
* __get() вызывается в случае, если код пытается считать данные из несуществующих или недоступных свойств объекта
* __set() вызывается при попытке присвоить данные недоступным или несуществующим свойствам объекта
* __isset() будет выполнен при использовании isset() или empty() на недоступных (защищённых или приватных) или несуществующих свойствах
* __unset() будет выполнен при вызове unset() на недоступном (защищённом или приватном) или несуществующем свойстве
* __sleep() вызывается во время обращения к объекту с помощью функции serialize(). В случае очень большого объекта требуется сохранить лишь выбранные свойства во время сериализации и после этого закрыть объект. Метод __sleep() в таком случае возвращает массив с именами всех свойств объекта, которые должны быть сериализированы (преобразованы в специальную строку).
* __wakeup() используется для восстановления связей с объектами и выполнения заданий после того, как передача данных (сериализация) закончена и для объекта вызывается функция unserialize()
* __toString() позволяет классу решать, как он должен реагировать при преобразовании в строку. Например, что вывести при выполнении echo $obj;
* __invoke() вызывается, когда скрипт пытается выполнить объект как функцию
* __set_state() используется в связке с функцией var_export(). Данная функция выводит структурированную информацию о переменной. Если вы используете функцию var_export() для экспорта класса, вам необходимо определить в нем метод __set_state()
* __clone() при клонировании объекта, PHP выполняет поверхностную копию всех свойств объекта. Любые свойства, являющиеся ссылками на другие переменные, останутся ссылками. После завершения клонирования, если метод __clone() определён, то будет вызван метод __clone() вновь созданного объекта для возможного изменения всех необходимых свойств
* __debugInfo() Этот метод вызывается функцией var_dump(), когда необходимо вывести список свойств объекта. Если этот метод не определён, тогда будут выведены все свойства объекта c модификаторами public, protected и private

**[⬆ вернуться к началу](#содержание)**

## Что такое генераторы и как их использовать?
Генераторы предоставляют лёгкий способ реализации простых итераторов без использования дополнительных ресурсов.

Генератор позволяет писать код, использующий foreach для перебора набора данных без необходимости создания массива в памяти, что может привести к превышению лимита памяти, либо потребует довольно много времени для его создания. Вместо этого, вы можете написать функцию-генератор, которая, по сути, является обычной функцией, за исключением того, что вместо возврата единственного значения, генератор может возвращать (yield) столько раз, сколько необходимо для генерации значений, позволяющих перебрать исходный набор данных.

Пример:
```php
function someFunc() 
{
    foreach (range(0, 1000000) as $value) {
        echo $value;
    }
}
someFunc(); // Fatal error: Allowed memory size of 134217728 bytes exhausted
```
Закончилась память!

Так же функция с генератором будет работать:

```php
function someFunc()
{
    foreach (range(0, 1000000) as $value){
        yield $value;
    }
}

var_dump(someFunc()); // object(Generator)[1]
foreach (someFunc() as $value){
    echo $value;
}
```
Генератор - функция с хранимым состоянием. Генератор выполняется до следующего слова yield в коде, где выбрасывает рассчитанное значение значение наружу и "засыпает", ожидая следующего вызова, чтобы потом продолжить с прерванной точки. С помощью генератора можно реализовать поддержку эффективных по памяти бесконечных последовательностей, по типу ряда Фибоначчи или гармонических рядов.
Генераторы могут пригодиться когда необходимо обработать большие объемы данных (например, файлы логов), выполнить вычисления на больших выборках из базы и т.д. И мы не хотим, чтобы эти операции занимали всю доступную память. Использование слова return в генераторе полностью останавливает его, после чего генератор нельзя уже будет пробудить повторно.


```php
function someFunc()
{
    foreach (range(0, 1000000) as $value){
        $signal = yield $value;
        if ($signal === 'stop') {
            return;
        }
    }
}

$generator = someFunc();
foreach($generator as $range) {
    if ($range === 100) { 
        $generator->send('stop');
    } 
}
```

Функции-генераторы могут содержать несколько yield

```php
function exampleGenerator() {
    yield 1;
    yield 2;
    yield 3;
}
 
$generator = exampleGenerator();
foreach ($generator as $value) {
    echo $value;
}
// Выведет: 123
```

**[⬆ вернуться к началу](#содержание)** 


### Что такое traits? Альтернативное решение? Приведите пример.
Трейт - это механизм обеспечения повторного использования кода в языках с поддержкой только одиночного наследования, таких как PHP.
Наследуемый член из базового класса переопределяется членом, находящимся в трейте. Порядок приоритета следующий: члены из текущего класса переопределяют методы в трейте, которые в свою очередь переопределяют унаследованные методы.
В трейтах можно определять статические переменные, статические методы и статические свойства.

**[⬆ вернуться к началу](#содержание)**

### Опишите поведение при использовании traits с одинаковыми именами полей или методов.

Если два трейта добавляют метод с одним и тем же именем, это приводит к фатальной ошибке в случае, если конфликт явно не разрешён.

Для разрешения конфликтов именования между трейтами, используемыми в одном и том же классе, необходимо использовать оператор insteadof для того, чтобы точно выбрать один из конфликтующих методов.

**[⬆ вернуться к началу](#содержание)**

### Будут ли доступны частные методы trait в классе?
Будут. Пример:
```php
trait helloTrait
{
    private function sayHello()
    {
        echo "Hello from trait";
    }
}

class myClass
{
    use helloTrait;

    public function hello()
    {
        $this->sayHello();
    }
}

$obj = new myClass();
$obj->hello(); // Hello from trait
```

**[⬆ вернуться к началу](#содержание)**

### Можно ли компоновать traits в trait?
Трейты могут использоваться и в других трейтах. Используя один или более трейтов в определении другого трейта, он может частично или полностью состоять из членов, определённых в этих трейтах.

**[⬆ вернуться к началу](#содержание)**

## Middle

## Senior