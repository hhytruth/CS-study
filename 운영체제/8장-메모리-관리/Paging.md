### Paging Example
- Paging
  + 프로세스의 가상 메모리를 동일한 사이즈의 페이지 단위로 나눔
  + 가상 메모리의 내용이 페이지 단위로 noncontiguous하게 저장됨
  + physical memory를 동일한 크기의 frame으로 나눔
  + logical memory를 동일 크기의 page로 나눔(frame과 같은 크기)
  + External fragmentation 발생 안함
  + Internal fragmentation 발생 가능

### Address Translation Architecture   
![image](https://user-images.githubusercontent.com/28378553/125285478-a5e67000-e355-11eb-80f1-e1af93ba5bc7.png)
- 

### Implementation of Page Table   
![image](https://user-images.githubusercontent.com/28378553/125285381-8ea78280-e355-11eb-8c7d-cadbc2ca9ecf.png)
- Page table은 메인 메모리에 상주
- Page-table base register(PTBR)가 page table을 가리킴
- Page-table length register(PTLR)가 테이블 크기를 보관
- 속도 향상을 위해 associative register 혹은 translation look-aside buffer(TLB)라 불리는 고속의 lookup hardware cache 사용

### Paging Hardware with TLB   
![image](https://user-images.githubusercontent.com/28378553/125285916-24431200-e356-11eb-95bd-2e38d65ce738.png)
- Effective Access Time   
![image](https://user-images.githubusercontent.com/28378553/125286163-6f5d2500-e356-11eb-8ecf-5d8505e079f3.png)

### Two-Level Page Table   
![image](https://user-images.githubusercontent.com/28378553/125286258-91ef3e00-e356-11eb-9692-116ec97360ad.png)
- page table 자체를 page로 구성
- 사용되지 않는 주소 공간에 대한 outer page table의 엔트리 값은 NULL(대응하는 inner page table이 없음)
- Address-Translation Scheme
- Two-Level Paging Example   
![image](https://user-images.githubusercontent.com/28378553/125286679-0f1ab300-e357-11eb-9ce2-755b20ef0af0.png)   
![image](https://user-images.githubusercontent.com/28378553/125286773-235eb000-e357-11eb-91bc-d3299eb16754.png)

### Multilevel Paging and Performance
- Address space가 더 커지면 다단계 페이지 테이블 필요

### Valid (v)/ Invalid (i) Bit in a Page Table   
![image](https://user-images.githubusercontent.com/28378553/125287047-6fa9f000-e357-11eb-9115-bd3877e13191.png)
- Valid는 해당 주소의 프레임에 그 프로세스를 구성하는 유효한 내용이 있음을 뜻함(접근 허용)
- Invalid는 해당 주소의 프레임에 유효한 내용이 없음을 뜻함(접근 불허)
  + 프로세스가 그 주소 부분을 사용하지 않는 경우
  + 해당 페이지 메모리에 올라와 있지 않고 swap area에 있는 경우

### Inverted Page Table
- Inverted Page Table Architecture   
![image](https://user-images.githubusercontent.com/28378553/125287571-0ecee780-e358-11eb-9952-6733126f0584.png)    
페이지 테이블이 프로세스당 하나씩 존재하는 것이 아니라 시스템 내에 하나 존재

### Shared Page
- Shared Pages Example    
![image](https://user-images.githubusercontent.com/28378553/125287769-4c337500-e358-11eb-88a1-cf63483984fd.png)
  + read-only로 하여 프로세스 간에 하나의 code만 메모리에 올림
  + Shared code은 모든 프로세스의 logical address space에서 동일한 위치에 있어야 함
