### Segmentation Architecture
- 프로그램은 의미 단위인 여러 개의 segment로 구성(logical unit)
- Logical address는 다음의 두 가지로 구성: segment-number, offset
- Segment table
  + each table entry has:
  + base-starting physical address of the segment
  + limit-length of the segment
- Segment-table base register(STBR): 물리적 메모리에서의 세그먼트 테이블의 위치
- Segment-table length register(STLR): 프로그램이 사용하는 세그먼트의 수
  + segment number s is legal if s<STLR

### Segmentation Hardware   
![image](https://user-images.githubusercontent.com/28378553/125288406-1478fd00-e359-11eb-9a4d-9b416e1b969b.png)
- Segment는 의미 단위이기 때문에 공유와 보안에 있어 paging보다 훨씬 효과적이다
- Allocation
  + first fit/best fit
  + external fragmentation 발생

### Example of Segmetation    
![image](https://user-images.githubusercontent.com/28378553/125289108-cf08ff80-e359-11eb-9888-781a8219a95c.png)

### Sharing of Segments   
![image](https://user-images.githubusercontent.com/28378553/125289220-f6f86300-e359-11eb-8647-8d1663a94f37.png)

### Segmentation with Paging
- pure segmentation과의 차이점: segment-table entry가 세그먼트의 base address를 가지고 있는 것이 아니라 세그먼트를 구성하는 페이지 테이블의 base address를 가지고 있음
- External fragmentation이 발생하지 않음   
![image](https://user-images.githubusercontent.com/28378553/125289544-4f2f6500-e35a-11eb-8e0f-e286fd38aecf.png)
