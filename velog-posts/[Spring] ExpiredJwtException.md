<p>jwt 토큰 로그인 방식을 구현하다가 access token이 만료됐는 지 확인하는 메서드가 필요해서 구현을 했었다.</p>
<pre><code class="language-java">public boolean isExpired(String token, String secretKey) {
    return getClaims(token, secretKey).getExpiration().before(new Date());
    }</code></pre>
<p>이런 식의 코드였는데, 문제는 여기서 라이브러리가 자동으로 만료 에러를 throw한다는 것이었다. 난 만료 됐는지 안됐는지 참거짓만 알면되는데 말이다. 그래서 결국 </p>
<pre><code class="language-java">public boolean isExpired(String token, String secretKey) {
        try{
            return getClaims(token, secretKey).getExpiration().before(new Date());
        } catch (ExpiredJwtException e){
            return true;
        }
    }</code></pre>
<p>try catch 문으로 예외처리를 해줬다.</p>