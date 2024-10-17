<p>자바를 하면서 항시 드는 생각인데, dto에서 entity 왔다갔다 하는 일이 필요할 때, builer를 써주는 게 맞는지 아님 dto를 인자로 받는 생성자를 entity에서 생성해주는 것이 맞는지 항상 고민이었다.</p>
<h2 id="builder">builder</h2>
<pre><code class="language-java">Seminar seminar = Seminar.builder()
                         .seminarDate(localDate)
                         .presentorList(new ArrayList&lt;&gt;())
                         .build();
</code></pre>
<p>말그대로 클래스 안에 buider 어노테이션이 들어간 메서드(생성자)를 만들어서 다음과 같이 생성할 수 있게 해주는 코드이다.</p>
<h3 id="장점">장점</h3>
<ul>
<li>가독성이 좋다</li>
<li>유연성 - 필드 순서 상관없이 매개변수 개수 상관없이 활용하기 좋다</li>
<li>확장성이 좋다</li>
</ul>
<h2 id="생성자">생성자</h2>
<pre><code class="language-java">Seminar seminar = new Seminar(dto);</code></pre>
<p>dto를 넘기면 생성자에서 dto에서 getter로 필드들을 빼내서 entity의 필드에 설정해주는 방식이다.</p>
<h3 id="장점-1">장점</h3>
<ul>
<li>여러 레이어를 오가면서 데이터가 이동될 때 편함</li>
<li>객체 생성과 관련된 로직을 구분하기 좋음</li>
</ul>