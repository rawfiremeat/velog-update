<p>때는 프로젝트 중에 각 entity들의 join 관계를 다시 만져보고 있던 중.</p>
<p>본래 프로젝트 개발을 진행할 때 백엔드 나 포함 2명이서 진행했고,
내가 로그인과 유저, 다른 팀원이 나머지 기능 2개를 구현하는 식으로 기능별로 개발을 분담했다.
때문에 각 기능별로 연관되어있는 entity들의 join은 뒤로 미루고 독립적으로 개발하게 된 것.</p>
<p><img alt="" src="https://velog.velcdn.com/images/9409velog/post/afe1014b-f187-4457-9c0b-f29f33d1e6c0/image.png" /></p>
<p>초기 erd가 이런 식이었다. user과 다른 기능에 대한 두 개의 table이 각각 일대다로 join하고 있는구조. </p>
<p>처음엔 이를 연결하려고 다(多) 쪽의 테이블에다만 연결하는 annnotation을 달아놨었다.
<img alt="" src="https://velog.velcdn.com/images/9409velog/post/f2eae569-8869-47ea-8fbf-e78154964c96/image.png" /></p>
<p>헌데 이렇게 하니까 join은 됐는데, 부모격 table인 user에 있는 row 즉 record 를 지우려고 시도하면 constraint 제약 조건 때문에 삭제가 진행되지 않는 것이다.</p>
<p>그렇다 작년 db 수업 때 배웠던 것이 나왔다. 아마 저렇게 다(多) 쪽의 테이블에서만 참조 기능을 하는 코드를 넣어주면 아마 제약조건이 restrict로 생성되는 것 같았다.</p>
<p>해서 제약조건을 spring에서 설정해 줄 수 있는 방법은 일(1) 쪽의 테이블에서 해줘야 한다는 것을 깨닫고 코드를 넣어줬다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/9409velog/post/0388e1e5-1d5a-44a6-99cb-0d4eb479f58e/image.png" /></p>
<p>여기서부터 본격적인 문제가 발생하기 시작했던 것 같은데, 아마 위에서 내가 이미 table의 관계를 생성한 채로 table을 만들었고, 난 그것을 다 갈아업고 새로운 제약조건으로 이루어진 table 관계를 만들고 싶었던 것인 와중에 계속해서 </p>
<pre><code>Hibernate: 
    alter table ledger 
       drop 
       foreign key FK5n5ykmim3npf1nawn1t0mmgwi
2024-07-29T16:22:25.985+09:00  WARN 93089 --- [           main] o.h.t.s.i.ExceptionHandlerLoggedImpl     : GenerationTarget encountered exception accepting command : Error executing DDL &quot;
    alter table ledger 
       drop 
       foreign key FK5n5ykmim3npf1nawn1t0mmgwi&quot; via JDBC [Table 'memory.ledger' doesn't exist]

org.hibernate.tool.schema.spi.CommandAcceptanceException: Error executing DDL &quot;
    alter table ledger 
       drop </code></pre><p>이런 에러가 뜨는 것이다. 너의 참조키를 삭제할 수 없다. 너의 참조키를 찾을 수 없다. 쉽게 말하자면 이미 내가 db에대가 똑같은 이름의 테이블을 다른 제약조건을 가진채로 넣어놔서 삭제할 수 없다는 것이다. </p>
<p>아니 이게 웬,, 그냥 지우면 되는 거 아닌가? 라고 생각했다. 그래서 제약키 조건 자체를 sql에서 수동적으로 지워줘도 보고 실제로 수동으로 다(多) 쪽의 테이블을 지워도 봤는데 똑같은 에러가 떴다. 근데 다시 생각해보니 간단한 곳에 답이 있었다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/9409velog/post/d2ff5bef-cb4f-4203-9fcb-9e01d059f4f7/image.png" /></p>
<p>이 부분은 개발 편하게 하려고 임시로 넣어놓은 데이터인데, 이게 먼저 자꾸 생성되어서 이미 데이터와 제약조건이 생겨버린 테이블을 지우라고 하니까 spring이 싫어했던 것이었다. 저 부분을 주석 처리해주고, 기존에 있던 테이블에 row들을 정리한다음 ddl-auto를 create로 바꾸고 해보니 잘 됐다.</p>