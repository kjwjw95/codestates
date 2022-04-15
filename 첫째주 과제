package com.example.demo;

import static org.junit.jupiter.api.Assertions.*;

import java.time.Duration;

import org.junit.jupiter.api.Test;

import reactor.core.publisher.Flux;
import reactor.test.StepVerifier;
import reactor.util.function.Tuple2;

class tests {
//["Blenders", "Old", "Johnnie"] 와 "[Pride", "Monk", "Walker”] 를 순서대로 하나의 스트림으로 처리되는 로직 검증
	@Test
	public void first(){
		Flux<String> names1$ = Flux.just("Blenders", "Old", "Johnnie")
				.delayElements(Duration.ofSeconds(1));
		Flux<String> names2$ = Flux.just("Pride", "Monk", "Walker")
				.delayElements(Duration.ofSeconds(1));
		Flux<String> names$ = Flux.concat(names1$, names2$)
				.log();
		
		StepVerifier.create(names$)
				.expectSubscription()
				.expectNext("Blenders", "Old", "Johnnie", "Pride", "Monk", "Walker")
				.verifyComplete();
	}
	//1~100 까지의 자연수 중 짝수만 출력하는 로직 검증
	@Test
	public void second(){
		Flux<Integer> names$ = Flux.range(1,30).filter(num->num%2==0).log();
		
		StepVerifier.create(names$)
				.expectSubscription()
				.expectNext(2,4,6,8,10,12,14,16,18,20,22,24,26,28,30)
				.verifyComplete();
	}
	//“hello”, “there” 를 순차적으로 publish하여 순서대로 나오는지 검증
	@Test
	public void third(){
		Flux<String> names$ = Flux.just("hello","there").log();
		
		StepVerifier.create(names$)
				.expectSubscription()
				.expectNext("hello","there")
				.verifyComplete();
	}
	//아래와 같은 객체가 전달될 때 “JOHN”, “JACK” 등 이름이 대문자로 변환되어 출력되는 로직 검증
	@Test
	public void fourth(){
		Flux<String> names$ = Flux.just(new Person("John","[john@gmail.com](mailto:john@gmail.com)",12345678),new Person("Jack","[jack@gmail.com](mailto:jack@gmail.com)",12345678))
				.map(p->{
					return p.name.toUpperCase();
				})
				.log();
		
		StepVerifier.create(names$)
				.expectSubscription()
				.expectNext("JOHN","JACK")
				.verifyComplete();
	}
	//["Blenders", "Old", "Johnnie"] 와 "[Pride", "Monk", "Walker”]를 압축하여 스트림으로 처리 검증
	@Test
	public void fifth(){
		Flux<String> names1$ = Flux.just("Blenders", "Old", "Johnnie");
		Flux<String> names2$ = Flux.just("Pride", "Monk", "Walker");
		Flux<String> names$ = Flux.zip(names1$,names2$,(s1,s2)->String.format("%s %s",s1,s2)).log();
		
		StepVerifier.create(names$)
				.expectSubscription()
				.expectNext("Blenders Pride","Old Monk","Johnnie Walker")
				.verifyComplete();
	}
	//["google", "abc", "fb", "stackoverflow”] 의 문자열 중 5자 이상 되는 문자열만 대문자로 비동기로 치환하여 1번 반복하는 스트림으로 처리하는 로직 검증
	@Test
	public void sixth(){
		Flux<String> names$ = Flux.just("google","abc","fb","stackoverflow")
				.map(p->{
					if(p.length()>=5) {
						return p.toUpperCase();
					}else {
						return p;
					}
				}).log();
		
		StepVerifier.create(names$)
				.expectSubscription()
				.expectNext("GOOGLE","abc","fb","STACKOVERFLOW")
				.verifyComplete();
	}
}
