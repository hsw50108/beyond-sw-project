![header](https://capsule-render.vercel.app/api?type=waving&color=timeGradient&text=🏠DOC%20(대학생%20원룸%20추천%20서비스%20)&animation=twinkling&fontSize=30&fontAlignY=40&fontAlign=70&height=250&fontAlign=50&fontAlignY=50 )
## "residence recommendation service for colleage students"

대학생들을 위한 원룸 추천 서비스입니다.



## 🙋 4team

정황엽 전예은 백승호 이윤경 김동욱


### 🏡 프로젝트 소개
**** ** **

대원추(대학생 원룸 추천 서비스)는 대학생들을 위한 주거 문제 해결을 위한 편의를 제공하는 서비스입니다. 

<p align="center">
<image src="https://digitalchosun.dizzo.com/site/data/img_dir/2018/03/12/2018031211894_0.jpg" width="200" height="200"/>  <image src="https://thumb17.iclickart.co.kr/Thumb17/16260000/16254533.jpg" width="200" height="200/">
</p>

<p align="center">
<image src="https://cdn.imweb.me/upload/S20200714abd6f1d9194e8/28c35bbdbc1e4.jpg" width="400" height="400"/>
</p>









사용자는 자신이 속한 학교를 기반으로 원하는 위치를 빠르게 선택할 수 있으며 편의시설(근처 시설), 가격대, 주거 형식 등을 고려하여 최적의 주거시설을 추천받을 수 있습니다. 
뿐만 아니라 사용자의 취향과 특별한 요구사항까지 고려하여 맞춤형 결과물을 제공합니다.
더불어 대원추는 자취하는 학생들 간의 교류와 안전을 고려하여 쉐어하우스 제도를 적극적으로 권장하고 있습니다.


### 🏠 프로젝트 상세 정보
**** ** **
대원추 시스템에 로그인 후 기본적인 인적사항 및 선호하는 매물 유형(예산, 매물 옵션, 편의시설 유무 등..)을 선택하면 그에 따라 매칭된 매물을 확인할 수 있습니다.





### 🏡 프로젝트 필요성
**** ** **

![lll](https://github.com/yun072/gitproject/assets/140836341/f7ebee14-d9bc-4a9f-8fc9-002f69a00e91)



2020년 대학생을 대상으로 한 자취계획 설문조사에 따르면 응답자 중 54%가 자취를 희망했으며 응답자들은 주로 '원거리 통학(45%)', '자유로운 생활(20.3%)','자기계발(18.2%)'등을 이유로 자취를 희망했습니다. 자취를 선택하지 않은 이들은 '온라인 개강 확대(32.1%)'를 가장 큰 이유로 꼽았으나 이는 2023년 6월부터 코로나19 위기 단계가 '심각'에서 '경계'로 조정되면서 확진자 격리 의무가 해제되었고, 
이에 따라 온라인 수업이 아닌 오프라인 수업으로 변경되면서 그 의미가 무색해졌다고 할 수 있습니다. 이로 인해 대학생들 중 자취를 선호하는 비율이 더 증가할 것으로 예상했습니다. 


### 📃 요구사항 명세서
**** ** **
![1](https://github.com/beyond-sw-camp/be05-1st-4team-DOC/assets/140836341/b24cce5e-f51e-4d8d-9cf7-d95be96422da)

![2222222](https://github.com/beyond-sw-camp/be05-1st-4team-DOC/assets/140836341/4c5cecd7-0d82-4e68-b0df-ef88aac96ae5)





### ⚙ DB 모델링
**** ** **
   
  ![image (1)](https://github.com/yun072/gitproject/assets/140836341/3b43aaa7-4f83-4ea1-8156-35fb8b2dfe9f)

### ⚙ DB 설계를 위한 DDL 구문
**** ** **
1) DDL 테이블 생성 구문
<pre>
<code>
USE DOC_CREATE;
-- TBL_LSSR
CREATE TABLE TBL_LSSR (
    LSSR_NO INT AUTO_INCREMENT PRIMARY KEY,
    LSSR_NM VARCHAR(100) NOT NULL,
    LSSR_TELNO VARCHAR(13) UNIQUE NOT NULL
);
-- TBL_BLDG
CREATE TABLE TBL_BLDG (
    BLDG_NO INT AUTO_INCREMENT PRIMARY KEY,
    BLDG_TYP VARCHAR(80) CHECK (BLDG_TYP IN ('HH_FC', 'UNIV', 'CM_FC'))
);
-- TBL_HH_FC
CREATE TABLE TBL_HH_FC (
    HH_FC_NO INT PRIMARY KEY,
    HH_FC_NM VARCHAR(100) NOT NULL,
    LSSR_NO INT,
    FLOOR SMALLINT NOT NULL,
    BD_YMD DATE NOT NULL,
    FOREIGN KEY (HH_FC_NO) REFERENCES TBL_BLDG(BLDG_NO),
    FOREIGN KEY (LSSR_NO) REFERENCES TBL_LSSR(LSSR_NO)
);
-- TBL_AREA
CREATE TABLE TBL_AREA (
    HH_FC_NO INT PRIMARY KEY,
    GRAR DECIMAL(5, 2),
    XUAR DECIMAL(5, 2),
    FOREIGN KEY (HH_FC_NO) REFERENCES TBL_HH_FC(HH_FC_NO)
);
-- TBL_OPT
CREATE TABLE TBL_OPT (
    HH_FC_NO INT PRIMARY KEY,
    OPT VARCHAR(80) CHECK(OPT IN('인덕션', '싱크대', '에어컨', '신발장', '세탁기', '냉장고', '옷장', '책상', '침대', '전자레인지')),
   FOREIGN KEY (HH_FC_NO) REFERENCES TBL_HH_FC(HH_FC_NO)
);
-- TBL_UNIV
CREATE TABLE TBL_UNIV (
    UNIV_NO INT PRIMARY KEY,
    UNIV_NM VARCHAR(100) NOT NULL,
    FOREIGN KEY (UNIV_NO) REFERENCES TBL_BLDG(BLDG_NO)
);
-- TBL_CM_FC
CREATE TABLE TBL_CM_FC (
    CM_FC_NO INT PRIMARY KEY,
    CM_FC_TYP VARCHAR(80) NOT NULL CHECK(CM_FC_TYP IN ('편의점', '음식점', '카페' ,'PC방' ,'스터디카페' ,'술집', '노래방')),
    CM_FC_NM VARCHAR(100) NOT NULL,
    FOREIGN KEY (CM_FC_NO) REFERENCES TBL_BLDG(BLDG_NO)
);
-- TBL_ADDR
CREATE TABLE TBL_ADDR (
    BLDG_NO INT PRIMARY KEY,
    CPTV_NM VARCHAR(100),
    SGG_NM VARCHAR(100),
    DADDR	VARCHAR(100),
    FOREIGN KEY (BLDG_NO) REFERENCES TBL_BLDG(BLDG_NO)
);
-- TBL_CRDS
CREATE TABLE TBL_CRDS (
    BLDG_NO INT PRIMARY KEY,
    COORDS_LAT DECIMAL(9, 6) NOT NULL,
    COORDS_LON DECIMAL(9, 6) NOT NULL,
    FOREIGN KEY (BLDG_NO) REFERENCES TBL_BLDG(BLDG_NO)
);
-- TBL_USER
CREATE TABLE TBL_USER (
    USER_NO INT AUTO_INCREMENT PRIMARY KEY,
    USER_NM VARCHAR(100) NOT NULL,
    USER_RRNO VARCHAR(14) UNIQUE,
    UNIV_NO INT,
    FOREIGN KEY (UNIV_NO) REFERENCES TBL_UNIV(UNIV_NO)
);
-- TBL_PRPT
CREATE TABLE TBL_PRPT (
    PRPT_NO INT AUTO_INCREMENT PRIMARY KEY,
    RES_TYP VARCHAR(80) CHECK (RES_TYP IN ('쉐어하우스', '원룸', '1.5룸', '투룸', '오피스텔')),
    CTRT_PRD INT,
    HH_FC_NO INT NOT NULL,
    PSTG_YMD DATE,
    FOREIGN KEY (HH_FC_NO) REFERENCES TBL_HH_FC(HH_FC_NO)
);
-- TBL_SHRH
CREATE TABLE TBL_SHRH (
    PRPT_NO INT PRIMARY KEY,
    GNDR VARCHAR(1) CHECK (GNDR IN ('1', '2')),
    CPCT SMALLINT NOT NULL,
    FOREIGN KEY (PRPT_NO) REFERENCES TBL_PRPT(PRPT_NO)
);
-- TBL_CO
CREATE TABLE TBL_CO (
    PRPT_NO INT PRIMARY KEY,
    CRCT_TYP VARCHAR(80) CHECK (CRCT_TYP IN ('전세', '월세')),
    MNG_CO INT,
    FOREIGN KEY (PRPT_NO) REFERENCES TBL_PRPT(PRPT_NO)
);
-- TBL_RPM
CREATE TABLE TBL_RPM (
    PRPT_NO INT PRIMARY KEY,
    RPM INT DEFAULT 0,
    DPS INT NOT NULL,
    FOREIGN KEY (PRPT_NO) REFERENCES TBL_PRPT(PRPT_NO)
);
-- TBL_JEONSE
CREATE TABLE TBL_JEONSE (
    PRPT_NO INT PRIMARY KEY,
    DPS INT NOT NULL,
    FOREIGN KEY (PRPT_NO) REFERENCES TBL_PRPT(PRPT_NO)
);
-- TBL_REA
CREATE TABLE TBL_REA (
    REA_NO INT AUTO_INCREMENT PRIMARY KEY,
    REA_NM VARCHAR(100) NOT NULL,
    REA_SRT_NM VARCHAR(100) NOT NULL,
    REA_TELNO VARCHAR(13) UNIQUE NOT NULL
);
-- TBL_PRPT_REAdoc_create
CREATE TABLE TBL_PRPT_REA (
    PRPT_NO INT,
    REA_NO INT,
    PRIMARY KEY (PRPT_NO, REA_NO),
    FOREIGN KEY (PRPT_NO) REFERENCES TBL_PRPT(PRPT_NO),
    FOREIGN KEY (REA_NO) REFERENCES TBL_REA(REA_NO)
);
</code>
</pre>


### ❗ 설계 검증을 위한 테스트 
**** ** **

 1) CRUD 작업 테스트 케이스 명세서
   
![3](https://github.com/beyond-sw-camp/be05-1st-4team-DOC/assets/140836341/ed45694e-f120-4569-a469-a19a18bfb130)
![캡처4](https://github.com/beyond-sw-camp/be05-1st-4team-DOC/assets/140836341/e65cd74e-eb21-47bf-ad1e-3843242d39fa)




