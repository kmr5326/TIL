## Ubuntu nftables로 포트포워딩 적용하기
1. NAT 테이블/체인 생성
```sh
sudo nft add table ip nat
sudo nft 'add chain ip nat prerouting { type nat hook prerouting priority 0; }'
sudo nft 'add chain ip nat postrouting { type nat hook postrouting priority 100; }'
```
2. 네트워크 인터페이스 확인
```sh
ip link show
```

3. 포트포워딩 실행
```sh
sudo nft add rule ip nat prerouting iif {2번의 네트워크 인터페이스이름:ens5} tcp dport 80 redirect to 8080
```

4. 설정 확인
```sh
sudo nft list ruleset
// 아래처럼 나와야 합니다.
table ip nat {
        chain prerouting {
                type nat hook prerouting priority filter; policy accept;
                iif "ens5" tcp dport 80 redirect to :8080
        }
```
5. 인스턴스 재부팅 이후에도 반영되도록 설정
```sh
sudo apt install nftables -y
sudo systemctl enable nftables
sudo sh -c "nft list ruleset > /etc/nftables.conf"
```

### Java 빌드 war에서 jar로 변경하기

```groovy
build.gradle
/* ⛔️ 제거: WAR 프로젝트 전용 설정
id 'war'
providedRuntime 'org.springframework.boot:spring-boot-starter-tomcat'
*/


bootJar { enabled = true }      // (기본값이지만 명시 OK)
jar { enabled = false }         // plain.jar 만들지 않으려면 유지
```