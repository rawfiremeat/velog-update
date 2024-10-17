<h1 id="정리">정리</h1>
<p>코드가 길어서 선정리 후 문제 좀 하겠다.
처음에 풀 때는 뛰거나, 수영여부를 추상클래스로 하여서 할까도 생각하다가, 가능한 클래스에만 메서드를 정의하는 것으로 했었다. 
내가 듣는 강의 선생님의 코드를 보니, interface로 가능 여부를 명세하여 코드를 짰다.</p>
<h1 id="퀴즈">퀴즈</h1>
<ol>
<li>사람은 자식, 부모님, 조부모님이 있다.</li>
<li>모든 사람은 이름, 나이, 현재 장소정보(x,y좌표)가 있다.</li>
<li>모든 사람은 걸을 수 있다. 장소(x, y좌표)로 이동한다.</li>
<li>자식과 부모님은 뛸 수 있다. 장소(x, y좌표)로 이동한다.</li>
<li>조부모님의 기본속도는 1이다. 부모의 기본속도는 3, 자식의 기본속도는 5이다.</li>
<li>뛸때는 속도가 기본속도대비 +2 빠르다.</li>
<li>수영할때는 속도가 기본속도대비 +1 빠르다.</li>
<li>자식만 수영을 할 수 있다. 장소(x, y좌표)로 이동한다.</li>
</ol>
<hr />
<p>위 요구사항을 만족하는 클래스들을 바탕으로, Main 함수를 다음 동작을 출력( System.out.println )하며 실행하도록 작성하시오. 이동하는
동작은 각자 순서가 맞아야 합니다.</p>
<hr />
<ol>
<li>모든 종류의 사람의 인스턴스는 1개씩 생성한다.
P02-C04 Java 기초 39</li>
<li>모든 사람의 처음 위치는 x,y 좌표가 (0,0)이다.</li>
<li>모든 사람의 이름, 나이, 속도, 현재위치를 확인한다.</li>
<li>걸을 수 있는 모든 사람이 (1, 1) 위치로 걷는다.</li>
<li>뛸 수 있는 모든 사람은 (2,2) 위치로 뛰어간다.</li>
<li>수영할 수 있는 모든 사람은 (3, -1)위치로 수영해서 간다.</li>
</ol>
<h2 id="첫번째-코드">첫번째 코드</h2>
<h3 id="personjava">person.java</h3>
<pre><code class="language-java">public class Person {
    String name;
    int age, x, y, speed;

    public Person(String name, int age, int x, int y, int speed){
        this.name = name;
        this.age = age;
        this.x = x;
        this.y = y;
        this.speed = speed;
    }

    public void walk(int x, int y){
        this.x = x;
        this.y = y;
        getLocation();
    }
    public void getLocation() {
        System.out.println(name + &quot;: (&quot; + x + &quot;, &quot; + y + &quot;)&quot;);
    }
    public void getInformation(){
        System.out.println(name);
        System.out.println(age);
        System.out.println(speed);
        System.out.println(&quot;(&quot; + x + &quot;, &quot; +  y + &quot;)&quot;);
    }
}</code></pre>
<h3 id="grandparentjava">GrandParent.java</h3>
<pre><code class="language-java">public class GrandParent extends Person{

    public GrandParent(String name, int age, int x, int y, int speed) {
        super(name, age, x, y, speed);
    }

}</code></pre>
<h3 id="parentjava">Parent.java</h3>
<pre><code class="language-java">public class Parent extends Person{
    public Parent(String name, int age, int x, int y, int speed) {
        super(name, age, x, y, speed);
    }
    public void run(int x, int y){
        this.speed += 2;
        this.x = x;
        this.y = y;
        getLocation();
    }
}</code></pre>
<h3 id="childjava">Child.java</h3>
<pre><code class="language-java">public class Person {
    String name;
    int age, x, y, speed;

    public Person(String name, int age, int x, int y, int speed){
        this.name = name;
        this.age = age;
        this.x = x;
        this.y = y;
        this.speed = speed;
    }

    public void walk(int x, int y){
        this.x = x;
        this.y = y;
        getLocation();
    }
    public void getLocation() {
        System.out.println(name + &quot;: (&quot; + x + &quot;, &quot; + y + &quot;)&quot;);
    }
    public void getInformation(){
        System.out.println(name);
        System.out.println(age);
        System.out.println(speed);
        System.out.println(&quot;(&quot; + x + &quot;, &quot; +  y + &quot;)&quot;);
    }
}</code></pre>
<h3 id="mainjava">Main.java</h3>
<pre><code class="language-java">public class Main {
    public static void main(String[] args) {
        GrandParent grandParent = new GrandParent(&quot;aa&quot;, 72, 0, 0, 1);
        Parent parent = new Parent(&quot;bb&quot;, 50, 0, 0, 3);
        Child child = new Child(&quot;cc&quot;, 23, 0, 0, 5);

        grandParent.getInformation();
        parent.getInformation();
        child.getInformation();

        grandParent.walk(1,1);
        parent.walk(1,1);
        child.walk(1,1);

        parent.run(2, 2);
        child.run(2, 2);

        child.swim(3, -1);

    }
}</code></pre>
<h2 id="수정-코드">수정 코드</h2>
<h3 id="humanjava">Human.java</h3>
<pre><code class="language-java">public class Human {
    String name;
    int x, y;
    int age;
    int speed;

    public Human(String name, int x, int y, int age, int speed) {
        this.name = name;
        this.x = x;
        this.y = y;
        this.age = age;
        this.speed = speed;
    }

    public Human(String name, int age, int speed){
        this(name, 0, 0, age, speed);
    }

    public void printWhoAmI(){
        System.out.println(&quot;1)&quot; + name + &quot; 2)&quot; + age + &quot; 3)&quot; + getLocation() + &quot; 4)&quot; + speed);
    }
    public String getLocation() {
        return &quot;(&quot; + x + &quot;, &quot; + y + &quot;)&quot;;
    }

}
</code></pre>
<h3 id="grandparentjava-1">GrandParent.java</h3>
<pre><code class="language-java">public class GrandParent extends Human implements Walkable{
    public GrandParent(String name, int age) {
        super(name, age, 1);
    }

    @Override
    public void walk(int x, int y) {
        printWhoAmI();
        System.out.println(&quot;walk speed: &quot; + speed);
        this.x = x;
        this.y = y;
        System.out.println(getLocation());
    }
}
</code></pre>
<h3 id="parentjava-1">Parent.java</h3>
<pre><code class="language-java">public class Parent extends Human implements Walkable, Runnable{
    public Parent(String name, int age) {
        super(name, age, 3);
    }

    @Override
    public void run(int x, int y) {
        printWhoAmI();
        System.out.println(&quot;run speed: &quot; + (speed + 2));
        this.x = x;
        this.y = y;
        System.out.println(getLocation());
    }

    @Override
    public void walk(int x, int y) {
        printWhoAmI();
        System.out.println(&quot;walk speed: &quot; + speed);
        this.x = x;
        this.y = y;
        System.out.println(getLocation());
    }
}
</code></pre>
<h3 id="childjava-1">Child.java</h3>
<pre><code class="language-java">public class Child extends Human implements Walkable, Runnable, Swimmable{
    public Child(String name, int age) {
        super(name, age, 5);
    }

    @Override
    public void swim(int x, int y) {
        printWhoAmI();
        System.out.println(&quot;swim speed: &quot; + (speed + 1));
        this.x = x;
        this.y = y;
        System.out.println(getLocation());
    }

    @Override
    public void run(int x, int y) {
        printWhoAmI();
        System.out.println(&quot;run speed: &quot; + (speed + 2));
        this.x = x;
        this.y = y;
        System.out.println(getLocation());
    }

    @Override
    public void walk(int x, int y) {
        printWhoAmI();
        System.out.println(&quot;walk speed: &quot; + speed);
        this.x = x;
        this.y = y;
        System.out.println(getLocation());
    }
}</code></pre>
<h3 id="walkablejava">Walkable.java</h3>
<pre><code class="language-java">public interface Walkable {
    void walk(int x, int y);
}</code></pre>
<h3 id="runnablejava">Runnable.java</h3>
<pre><code class="language-java">public interface Runnable {
    void run(int x, int y);
}</code></pre>
<h3 id="swimmablejava">Swimmable.java</h3>
<pre><code class="language-java">public interface Swimmable {
    void swim(int x, int y);
}</code></pre>
<h3 id="mainjava-1">Main.java</h3>
<pre><code class="language-java">public class Main {
    public static void main(String[] args) {
        Human grandParent = new GrandParent(&quot;aa&quot;, 77);
        Human parent = new Parent(&quot;bb&quot;, 49);
        Human child = new Child(&quot;cc&quot;, 24);

        Human[] humans = {grandParent, parent, child};

        for(Human human:humans){
            human.printWhoAmI();
        }

        System.out.println(&quot;시작&quot;);

        for(Human human:humans){
            if (human instanceof Walkable){
                ((Walkable) human).walk(1, 1);
            }
            if (human instanceof Runnable){
                ((Runnable) human).run(2,2);
            }
            if (human instanceof Swimmable){
                ((Swimmable) human).swim(3,-1);
            }
        }
    }
}</code></pre>