# ComparatorLambdaOCP3
Comparator является функциональным интерфейсом, поскольку существует только один абстрактный метод для реализации.
Это означает, что мы можем переписать компаратор из предыдущего примера, использовав лямбды:

Компаратор
Иногда вы хотите отсортировать объект, который не реализован Comparable, или вы хотите отсортировать объекты по-разному в разное время.
Предположим, что мы добавляем weightв наш Duckкласс. Теперь у нас есть следующее:
public class Duck implements Comparable<Duck> { 
  private String name; 
  private int weight; 
  public Duck(String name, int weight) { 
     this.name = name;   
   this.weight = weight;
   } 
  public String getName() {  
return name;
 }  
 public int getWeight() { 
 return weight; 
} 
  public String toString() {
 return name; 
}  
public int compareTo(Duck d) {
      return name.compareTo(d.name); 
  }}
Сам Duckкласс может быть определен compareTo()только одним способом. В этом случае nameбыл выбран. Если мы хотим отсортировать что-то еще, мы должны определить этот порядок сортировки вне compareTo()метода:

public static void main(String[] args) {  
 Comparator<Duck> byWeight = new Comparator<Duck>() { 
     public int compare(Duck d1, Duck d2) {  
       return d1.getWeight()—d2.getWeight(); 
     } 
  };
   List<Duck> ducks = new ArrayList<>();
   ducks.add(new Duck("Quack", 7));
   ducks.add(new Duck("Puddles", 10)); 
  Collections.sort(ducks); 
  System.out.println(ducks);             // [Puddles, Quack]
   Collections.sort(ducks, byWeight); 
  System.out.println(ducks);             // [Quack, Puddles]
}
Сначала мы определили внутренний класс с помощью компаратора. Затем мы отсортировали без компаратора и с компаратором, чтобы увидеть разницу в выходе.
Comparatorявляется функциональным интерфейсом, поскольку существует только один абстрактный метод для реализации. Это означает, что мы можем переписать компаратор в предыдущем примере как любой из следующих:

Comparator<Duck> byWeight = (d1, d2) -> d1.getWeight()—d2.getWeight();
Comparator<Duck> byWeight = (Duck d1, Duck d2) -> d1.getWeight()—d2.getWeight();
Comparator<Duck> byWeight = (d1, d2) -> { return d1.getWeight()—d2.getWeight(); };
Comparator<Duck> byWeight = (Duck d1, Duck d2) -> {return d1.getWeight()—d2.getWeight(); };
Все эти примеры показывают, что принимают два параметра и возвращают - intкак Comparatorуказано. Помните, что тип является необязательным. Java выведет это по тому, что необходимо в этом месте кода. Это здорово. Вы можете переписать пять строк кода, используя фанк-синтаксис, в одну строку с другим фанк-синтаксисом! Это действительно круто, потому что вы привыкаете к лямбда-синтаксису, тогда как анонимный внутренний класс всегда чувствует себя глупо. В этой книге мы будем использовать сочетание лямбд и анонимных внутренних классов, так как вы должны увидеть оба подхода на экзамене.
