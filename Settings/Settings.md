1. Install SublimeText 3 & Sublime Merge  
- download sublimetext 3 dmg file  
move to https://www.sublimetext.com/3  
download OS X.dmg  
- download sublime merge dmg file  
move to https://www.sublimemerge.com/ and download file  
  
2. Programmers Compile Option  
*signal: illegal instruction (core dumped)*
위 오류는 컴파일 옵션을 지키지 않을 경우, 발생한다.  
swift의 경우, tensorflow를 설치해주어야 한다.  

3. Install Tensorflow  
*출처: https://www.tensorflow.org/install/pip?hl=ko#mac-os_1*  
  
- homebrew 설치  
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"  
- pip 설치  
sudo easy_install pip  
- python 설치  
brew install python  
- virtualenv 설치
python -m pip install --user virtualenv  
- python 가상환경 구성하기  
virtualenv --system-site-packages -p python3 ./venv  
*virtualenv 위치: ~/Python/2.7/bin*  
- 가상환경 활성화  
source ./venv/bin/activate  
*virtualenv가 활성화되면 셸 프롬프트가 (venv)로 시작한다. 호스트 시스템 설정에 영향을 주지 않고 가상 환경 내에 패키지를 설치한다.  
virtualenv를 종료하려면 다음을 실행한다. deactivate*  
- pip 패키지 업데이트  
pip install --upgrade pip. 
pip list  # show packages installed within the virtual environment.  
- tensorflow pip 패키지 설치  
pip install --upgrade tensorflow  