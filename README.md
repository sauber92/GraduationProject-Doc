# GraduationProject-Doc

> 2017-1 경희대학교 전자공학과 창의적설계(지도교수 김동한), 팀 608호 : 문서 레파지토리

***

## 프로젝트 소개

### 프로젝트 명  
전자석을 이용한 타자 연습기   

![](https://github.com/sauber92/GraduationProject-Doc/blob/master/Documentation/Reference/TA-icon/icon.png?raw=true)  

### 시스템 구성도  

![](https://github.com/sauber92/GraduationProject-Doc/blob/master/Documentation/Reference/Diagram/system.png?raw=true)  

**전자석을 이용한 타자 연습기**는 컴퓨터 응용프로그램인 *Typing Assistant*와 키보드 위에 올려놓고 사용하는 *Keyboard Panel*, 장갑형태의 *FingerTip*으로 이루어져있다.  

<br/>

### 시퀀스 다이어그램  

![](https://github.com/sauber92/GraduationProject-Doc/blob/master/Documentation/Reference/Diagram/sequence.png?raw=true)  

**과정 1,2**: 전원이 KP와 FT에 인가되면 KP와 FT은 서로 블루투스 연결을 맺는다. TA는 어플리케이션이 실행될 때 2초의 로딩시간을 거치면서 KP와 FT의 블루투스 연결이 맺어지는 것을 기다린다.  

**과정 3,4**: TA와 KP가 시리얼 연결을 맺는다.  

**과정 5,6**: TA는 입력해야 할 문자를 무작위로 생성한 후 모니터에 출력한다.  

**과정 7,8:** TA는 생성된 문자를 Character형으로 시리얼 통신을 통해 KP로 전달하고 KP는 이에 해당하는 전자석을 활성화한다.  

**과정 9,10**: KP는 TA로 부터 받은 문자를 블루투스 통신을 통해 FT으로 전달하고 FT은 이에 대항하는 전자석을 활성화한다.  

**과정 11**: 사용자가 KP와 FT의 전자석의 전자기력을 인지하고 키보드를 올바르게 입력하면 키보드 인터럽트 이벤트가 발생한다.  

**과정 12~15**: 키보드 인터럽트가 발생하면 KP와 FT의 전자석을 비활성화한다.  

**과정 16**: TA는 다시 새로운 문자를 무작위로 생성한 후 위의 과정을 반복한다.  

<br/>

***

## Typing Assistant  

### 소개  

![](https://github.com/sauber92/GraduationProject-Doc/blob/master/Documentation/Reference/Diagram/tp.png?raw=true)

TA는 Node.js 엔진과 Chromium 브라우져을 기반으로 데스크탑 어플리케이션을 제작할 수 있는 [Electron](https://electron.atom.io/)을 사용하여 만들어졌다.  

[node-serialport 모듈](https://github.com/EmergingTechnologyAdvisors/node-serialport)을 사용하여 KP과 시리얼 통신을 할 수 있게 하였으며, 자체적으로 랜덤하게 영어 소문자 하나를 생성하고, 그에 해당하는 키보드 인터럽트 이벤트가 발생하면 다시 새로운 문자가 생성되게 하였다.  

### 개발스펙  

* IDE: WebStorm (Ver. 2016.3.2)  
* NPM: Ver 4.2.0
* Node: Ver 7.10.0  
* Electron: Ver 1.4.1  
* electron-installer-dmg: Ver 0.2.1  
* electron-rebuild: Ver 1.4.0  
* electron-winstaller: Ver 2.5.2  
* Dependencies  
	* app: 0.1.0  
	* electron-packager: 8.7.0  
	* path: 0.12.7  
	* serialport: 4.0.7  

### Release  

* Mac 버전: [dmg파일](https://github.com/sauber92/GraduationProject-TA/releases/tag/1.0.0)  
	* macOS Sierra 10.12.5에서 확인  
* Windows 버전: [exe파일](https://github.com/sauber92/GraduationProject-TA/releases/tag/1.0.1)  
	* Windows 10 Pro 1703에서 확인
	* Pre-release: 설치파일의 생성을 못해서 Pre-release 버전으로 실행파일만 배포

### Git Repository  

[https://github.com/sauber92/GraduationProject-TA](https://github.com/sauber92/GraduationProject-TA)

***

## Keyboard Panel  

### 소개  

![](https://github.com/sauber92/GraduationProject-Doc/blob/master/Documentation/Reference/Diagram/KP.png?raw=true)  

Arduino Mega 보드와 16채널 릴레이 2개, 전자석 26개를 사용하여 구성하였다. 블루투스 모듈은 HC-06을 사용하였다.  

[SoftwareSerial 라이브러리](https://www.arduino.cc/en/Reference/softwareSerial)를 통해 FT과 블루투스 통신을 하였다.  

### 개발스펙  

* IDE: Arduino Sketch (Ver. 1.8.2)  
* Arduino Mega ADK
	* SoftwareSerail library  

### Git Repository  

[https://github.com/sauber92/GraduationProject-KP](https://github.com/sauber92/GraduationProject-KP)

***

## FingerTip

### 소개  

![](https://github.com/sauber92/GraduationProject-Doc/blob/master/Documentation/Reference/Diagram/FT.png?raw=true)  

Arduino Uno 보드와 4채널 릴레이 2개, 전자석 8개를 사용하여 구성하였다. 블루투스 모듈은 HC-06을 사용하였다.  

[SoftwareSerial 라이브러리](https://www.arduino.cc/en/Reference/softwareSerial)를 통해 KP과 블루투스 통신을 하였다.  

### 개발스펙  

* IDE: Arduino Sketch (Ver. 1.8.2)  
* Arduino Uno
	* SoftwareSerail library  

### Git Repository  

[https://github.com/sauber92/GraduationProject-FT](https://github.com/sauber92/GraduationProject-FT)

***

## 동영상  

* Typing Assitant 유투브 영상(업로드 17년 4월 20일): [https://youtu.be/p1Mg6t1OUfo](https://youtu.be/p1Mg6t1OUfo)  
* 전체 프로젝트 소개 유투브 영상(업로드 17년 6월 1일): [https://youtu.be/ZEWkTbEnWDc](https://youtu.be/ZEWkTbEnWDc)

***

## 발표자료  

[최종 발표자료(SlideShare) - 17.06.01](https://www.slideshare.net/JunyoungJung8/graduation-project-76655191)  

[창의적 종합설계 경진대회 발표자료(SldideShare) - 17.07.04](https://www.slideshare.net/JunyoungJung8/team608-77488804)  

***

## 프로젝트 관리  

[team608의 트렐로](https://trello.com/b/TO1BCMvY)  

***

## License 

* Doc: [MIT 라이센스](https://github.com/sauber92/GraduationProject-Doc/blob/master/LICENSE)  
* TA: [MIT 라이센스](https://github.com/sauber92/GraduationProject-TA/blob/master/LICENSE.md)  
* KP: [MIT 라이센스](https://github.com/sauber92/GraduationProject-KP/blob/master/LICENSE)  
* FT: [MIT 라이센스](https://github.com/sauber92/GraduationProject-FT/blob/master/LICENSE)  

***

## 제작자  

* 정준영: 경희대학교 전자공학과/컴퓨터공학과 12학번  
	* Mail: jjy920517@gmail.com  
	* Github: [https://github.com/sauber92](https://github.com/sauber92)  
	* Blog: [https://sauber92.github.io](https://sauber92.github.io)  
* 오종렬: 경희대학교 전자공학과 12학번  
	* Mail: ohjongryeol@naver.com  
	* Github: [https://github.com/JongYeolOH](https://github.com/JongYeolOH)  
* 윤상윤: 경희대학교 전자공학과 12학번  
	* Mail: sangyounyoun@naver.com  
	* Github: [https://github.com/SangyounYoun](https://github.com/SangyounYoun)  
 
