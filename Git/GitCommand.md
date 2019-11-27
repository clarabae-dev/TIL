#### 기존 커밋 내역 변경하기
- 커밋했던 내역의 커밋 해쉬 값 검색  
git log  
- 검색 시작 지점이 될 해쉬 값을 지정해 커밋 내역을 검색  
git rebase -i -p b4cac44  
- 커밋 내역에서 peek -> edit 으로 변경  
- 단일 커밋 내역 수정 (하단 예시는 작성자 변경)  
git commit --amend --author="clarabae-dev <clarabae.dev@gmail.com>"  
- 나머지 커밋 내역도 연속해서 수정  
git rebase --continue  