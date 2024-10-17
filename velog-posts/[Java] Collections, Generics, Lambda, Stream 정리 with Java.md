<h1 id="collections">Collections</h1>
<p>콜렉션 프레임 워크는 데이터를 다루는 자료구조를 사용하는 클래스의 집합이라고 생각하면 좋다. 기존에 사용이 불편했던 Array 보다 더 많은 기능을 활용함으로서 쉽게 개발할 수 있다.
collections 프레임워크의 클래스는 Collection을 implement하는 클래스나, interface이다. </p>
<h2 id="list">List</h2>
<p>순서가 있는 집합, 중복을 허용한다. ex) ArrayList</p>
<pre><code class="language-java">public static void main(String[] args) {
        List&lt;Integer&gt; list = new ArrayList&lt;&gt;();
        list.add(1);
           list.get(2); //인덱싱

</code></pre>
<h2 id="set">Set</h2>
<p>순서를 유지하지 않는 데이터 집합, 중복 허용하지 않음 ex)HashSet</p>
<pre><code>public static void main(String[] args) {
Set&lt;Integer&gt; integerSet = new HashSet&lt;&gt;();
integerSet.add(1);
integerSet.add(3);
integerSet.add(2);
integerSet.add(9);
integerSet.add(9);

Set&lt;String&gt; stringSet = new HashSet&lt;&gt;();
stringSet.add(&quot;LA&quot;);
stringSet.add(&quot;New York&quot;);
stringSet.add(&quot;LasVegas&quot;);
stringSet.add(&quot;San Francisco&quot;);

stringSet.add(&quot;LA&quot;) // ==&gt; 실제로는 추가 안됨</code></pre><h2 id="map">Map</h2>
<p>키와 value로 구성되는 데이터 특징 인덱싱이 아님 키값으로 vaule를 찾아냄 python의 dictionary와 유사</p>
<p>키는 distinct함 키에 대해서 value를 넣으면 마지막 값만 남음</p>
<pre><code class="language-java">Map&lt;Integer, String&gt; map = new HashMap&lt;&gt;();
map.put(1, &quot;apple&quot;);
map.put(2, &quot;berry&quot;);
map.put(3, &quot;cherry&quot;);
map.put(100, &quot;pineapple&quot;);

</code></pre>
<ul>
<li>containsKey(key): key를 가지고 있는 지에 대한 true/false 값 반환</li>
<li>get, remove (key): 해당 key 값에 대한 value를 가져오거나 제거</li>
</ul>
<h2 id="stack">Stack</h2>
<p>LIFO 방식의 데이터 자료구조임. 제일 마지막에 들어온 것이 첫번째로 나감</p>
<pre><code class="language-java">Stack&lt;Integer&gt; stack = new Stack&lt;&gt;();
stack.push(1);
stack.pop();</code></pre>
<p>push로 제일 뒤에 넣고, pop 으로 제일 마지막 값을 반환함</p>
<h2 id="queue">Queue</h2>
<p>FIFO 형식의 데이터 자료구조. 파이프 형태로 먼저 들어온게 먼저 나간다.</p>
<pre><code class="language-java">Queue&lt;Integer&gt; queue = new LinkedList&lt;&gt;();
queue.add(1);
queue.add(3);

System.out.println(queue.poll()); // Queue에서 객체를 꺼내서 반환</code></pre>
<p>add, poll로 삽입과 제거를 진행함. add가 맨 뒤에 넣기, poll이 가장 앞값 반환하기</p>
<h2 id="deque">Deque</h2>
<p>queue와 stack의 성질을 모두 가지고 잇는 자료 구조. </p>
<pre><code class="language-java">ArrayDeque&lt;Integer&gt; deque = new ArrayDeque&lt;&gt;();
        deque.addLast(1);
        deque.addFirst(2);
        deque.offerLast(3);
        deque.offerFirst(4);
        System.out.println(deque);
        deque.pollFirst();
        deque.pollLast();
        System.out.println(deque);</code></pre>
<p>addFirst/Last , pollFirst/Last로 삽입 제거 진행함. remove와 peek도 지원함</p>
<h1 id="generics">+Generics</h1>
<p>객체를 생성할 때 동작은 같은데, 타입만 다른 경우 따로 타입을 지정할 수 있는 기능
같은 List 지만 int용 String 용이 따로 있지 않고 인스턴스 생성시에 선언하는 것임.</p>
<pre><code class="language-java">public class Main {
public static void main(String[] args) {
List&lt;String&gt; list = new ArrayList();
Collection&lt;String&gt; collection = list;
}
}
</code></pre>
<p>제네릭스는 꺽쇠(&lt;&gt;)안에 타입을 지정해주는 방식으로 사용함</p>
<h1 id="lambda">Lambda</h1>
<p>람다식은 식별자 없이 실행 가능한 함수라고 생각하면 됨. 함수 이름이나, 식별자를 따로 정의하지 않아도 간결하게 사용할 수 있는 것</p>
<pre><code class="language-java">public class Main {
public static void main(String[] args) {
ArrayList&lt;String&gt; strList = new ArrayList&lt;&gt;(Arrays.asList(&quot;korea&quot;, &quot;japan&quot;, &quot;china&quot;, &quot;france&quot;, &quot;england&quot;));
Stream&lt;String&gt; stream = strList.stream();
stream.map(str -&gt; str.toUpperCase()).forEach(System.out::println);
}
}
</code></pre>
<blockquote>
<p>이중 콜론 (::)
호출하고자 하는 함수의 파라미터 갯수와 각각의 타입이 lambda식에 전해지는 인자와 일치할 때 파라미터 값 입력을 생략하고 클래스의 함수만을 입력해서 사용할 수 있게 해준다.
위의 예제를 봤을 때 println의 파라미터 갯수와 foreach에서 전달되는 인자의 갯수가 같으므로 class::메서드 이런 식으로 사용이 가능하다.</p>
</blockquote>
<ul>
<li>람다식의 단점<ol>
<li>람다를 사용하여서 만든 익명 함수는 재사용이 불가능.</li>
<li>람다만을 사용할 경우 비슷한 메소드를 중복되게 생성할 가능성이 있으므로 지저분해질 수 있음.</li>
<li>로그를 보거나 디버깅을 하기 어려울 수 있음. 함수의 정확한 이름과 위치가 나타나지 않기 때문.</li>
</ol>
</li>
</ul>
<h1 id="stream">Stream</h1>
<p>fucntional 한 프로그래밍을 가능하게 해주는 도구임. 컬렉션의 저장요소를 하나씩 참조해서 람다식으로 처리할 수 있도록 해줌.
스트림은 원래 데이터 소스를 변경하지 않음. 작업을 내부적으로 반복 처리함. 컬렉션의 요소를 모두 읽고 끝나면 재사용이 불가능함. 재생성해야함</p>
<h2 id="스트림의-구조">스트림의 구조</h2>
<ol>
<li><p>스트림 생성 -&gt; 2. 중간 연산 -&gt; 3. 최종 연산</p>
</li>
<li><p>스트림 생성
말그대로 스트림을 생성하는 것임. Collection.stream으로 생성함</p>
</li>
<li><p>중간 연산
람다식을 이용해서 map, sort, filter 등의 가공을 하는 것임</p>
</li>
<li><p>최종 연산
요소를 모두 가공하고 그것을 최종적으로 반환하는 단계 컬렉션으로 반환 할 수 있음</p>
</li>
</ol>
<pre><code class="language-java">public static void main(String[] args) {
        List&lt;String&gt; names = Arrays.asList(&quot;김정우&quot;, &quot;김호정&quot;, &quot;이하늘&quot;, &quot;이정희&quot;, &quot;박정우&quot;, &quot;박지현&quot;, &quot;정우석&quot;, &quot;이지수&quot;);
        Stream&lt;String&gt; namestream = names.stream();

        long count = namestream.filter(name -&gt; name.startsWith(&quot;이&quot;))
                .count();
        System.out.println(count);
    }</code></pre>