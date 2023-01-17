<h2> Git 명령어 정리 </h2>
  <ul>
    <li>git --version: git 버전 확인</li>
    <li>git config --global user.name &ltusername&gt: 이름 설정</li>
    <li>git config --global user.email &ltuseremail&gt: 이메일 설정</li>
    <li>c:\&ltfile&gt: 파일 경로 설정</li>
    <li>git clone &lt http://github.com/username/file.git &gt: git 저장소 복제</li>
    <li>dir: 디렉토리 확인</li>
    <li>git add . or &ltfile&gt: 파일 추가</li>
    <li>git commit -m "&lt message &gt ": 깃허브 커밋 (메시지)</li>
    <li>git push: github upload</li>
    <li>git status: git 상태 확인</li>
    <li>git restore <file>: 수정된 내역 삭제 </li>
    <li>git commit --amend: commit message 수정</li>
    <li>esc + &lt :wq! &gt: commit message 수정 종료</li>
    <li>git pull: 저장소의 파일과 local 폴더를 일치시킴</li>
    <li>git log: 해시값으로 구성된 파일들의 상태를 확인할 수 있음</li>
    <li>git reset --hard &lt hash &gt: 특정 지점 이외는 모두 제거 (--soft, --mixed option도 있음)</li>
    <li>git push -f: 강제적으로 push</li>
    <li>git branch: branch 확인</li>
    <li>git branch &lt branchname &gt: branch 생성</li>
    <li>git checkout &lt branchname &gt: branch switch (git log 통해 작업 현황 확인)</li>
    <li>git checkout main -> git merge &lt branchname &gt -> git push: branch 병합 후 깃헙 업로드 </li>
    <li>git branch -d &lt branchname &gt: branch 삭제</li>
  </ul>
