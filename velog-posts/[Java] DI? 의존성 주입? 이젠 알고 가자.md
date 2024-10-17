<h1 id="🤨의존이란">🤨의존이란?</h1>
<p>의존한다. 객체지향에서 dependece는 곧 하나의 클래스나 객체가 다른 클래스나 객체의 도움으로 동작한다는 의미이다.</p>
<pre><code class="language-java">public class Store{
    private Paper paper;

    public Store (){
        this.paper = new Paper(); //의존한다
    }

    //paper 객체를 이용한 구현부
}</code></pre>
<p>이런 경우에 <code>Store</code>라는 객체가 <code>Paper</code>라는 객체에 의존한다라고 할 수 있다.</p>
<h2 id="❓문제가-되나">❓문제가 되나?</h2>
<p>이 경우 문제는 객체간의 의존성이 높다라는 것이다. 만약에 <code>paper</code>가 수정되거나 삭제되면 <code>store</code>도 영향을 받을 수 밖에 없는 법인 것이다. 때문에 의존성 주입이 중요하다고 할 수 있다.</p>
<h1 id="🤨의존성-주입이란">🤨의존성 주입이란?</h1>
<p>의존성 주입(Dependency Injection, DI)은 객체 지향 프로그래밍에서 객체 간의 의존성을 줄이고, 코드의 유연성과 재사용성을 높이기 위해 사용하는 디자인 패턴이다.</p>
<pre><code class="language-java">public class Store{
    private Paper paper;

    public Store (){
        this.paper = new Paper(); // 이 부분
    }

    //paper 객체를 이용한 구현부
}</code></pre>
<p>이 경우를 다시 보자. <code>Paper</code>에 의존하는 <code>Store</code> 가 직접 <code>Paper</code> 객체를 생성하는 것을 볼 수 있다. 이렇게 되면 의존성이 높아진다는 것이다.</p>
<p>해서 우리는 의존성 주입이란 것을 해줘야 한다.</p>
<h2 id="interface의-사용">interface의 사용</h2>
<p>DIP가 높은 의존성 주입을 할 때 용이한 것이 바로 interface이다.</p>
<p>객체간 의존성을 높이기 보다 더 추상화 수준이 높은 클래스들을 이용해서 코드의 유연성을 높이는 과정이라고 생각하면 된다.</p>
<pre><code class="language-java">public class Store{
    private Paper paper;

    public Store (){
        this.paper = new Paper(); // 이 부분
    }

    //paper 객체를 이용한 구현부
}</code></pre>
<p>나는 역할과 책임으로 봤을 때 가게와 종이는 추상화 정도가 다르다고 생각한다. 가게에선 종이를 파는 것이 역할이 아니다. 아예 틀린 말은 아니지만 가게에선 물건을 파는 것이다. 그렇기 때문에 나는 <code>Product</code>라는 인터페이스를 생성해서 보다 유연한 의존성 주입을 하려고 한다.</p>
<pre><code class="language-java">public interface Product {
    //void ~
}</code></pre>
<p>그리고 <code>Paper</code>가 <code>Product</code>를 구현한다.</p>
<pre><code class="language-java">public class Papter implements Product {
    //public void ~
}</code></pre>
<p>가게에 대한 내용도 바꾸어 준다</p>
<pre><code class="language-java">public class Store{
    private Product product;

    public Store (Product product){
        this.product = product;
    }

    //product 객체를 이용한 구현부
}</code></pre>
<p>그리고 나서 외부에서 가게를 생성하고 의존성을 주입해주려고 한다.</p>
<pre><code class="language-java">public class Main {
    public static void main(String[] args) {
        Product product = new Paper();  // product 객체를 주입
        Store store = new Store(product);
    }
}</code></pre>
<p>이렇게 되면 <code>Paper</code>에 대한 구현이 바뀌어도 <code>Store</code>를 바꿀 필요가 없어진다. 상대적으로 구체에 해당하는 <code>Paper</code> 구현부에서 수정이 많이 일어날 것을 생각하면 합리적인 수정이 된 것이다.</p>
<h1 id="dip">DIP??</h1>
<p>이 부분은 사실 객체지향의 SOLID에서 DIP(Dependency Inversion Principle) 법칙의 예시라고 할 수 있는 부분이다. 객체지향의 추구점인 '추상화', '추상화 수준의 통일', '코드의 결합도를 줄이는', '의존성을 줄이는', '다형성을 높이는' 뭐 이런 말들을 대표한다고 하면 된다. solid에 대한 공부가 더 완료되면 정리하도록 하겠다.</p>