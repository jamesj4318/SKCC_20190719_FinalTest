# Prequal 실습 (첨부파일 참고 부탁드립니다.)
## 1. System Configuration Check
```
1. Check vm.swappiness on all your nodes
 1) swap 확인 
  -> sysctl vm.swappiness
 2) 영구 적용 위해 /etc/sysctl.conf 추가 필요 
  -> vi /etc/sysctl.conf --> vm.swappiness = 1 추가
