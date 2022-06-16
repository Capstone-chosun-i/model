# 컴퓨터공학과 20174221 이현준
## 산학캡스톤디자인1

#### 주제 : 기온별 패션 추천 웹사이트

<img width="300" alt="KakaoTalk_20220616_160145216" src="https://user-images.githubusercontent.com/96337129/174116588-655fb5f6-aec7-4386-9f70-0f6dd70109d1.png"/>

#### 캡스톤디자인 발표자료
* 4월 15일 발표 PPT 자료
* 6월 3일 발표 PPT 자료

## 4월 15일 발표 내용
* 주제 설명
  * 주제 선정 이유
  * 카테고리 설명
<img width="432" alt="화면 캡처 2022-06-17 013719" src="https://user-images.githubusercontent.com/96337129/174122114-73f46733-19ff-472e-8126-a352d17a82e1.png">


* 웹 페이지 구조 및 기능 구상
  * 기온에 따라 옷 종류 매칭 
  * 기온에 따른 옷 추천
  * 이미지 업로드 및 분석
<img width="268" alt="화면 캡처 2022-06-17 013811" src="https://user-images.githubusercontent.com/96337129/174122032-b28acab9-cced-4639-8749-6cd19c53c2d3.png">

* 크롤링
  * 크롤링을 사용한 데이터 수집 

구글
```c
from distutils.log import error
from urllib.request import urlopen
from urllib.parse import quote_plus
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
import time
import os 
import urllib.request
def get_files_count(folder_path):
    list=os.listdir(folder_path)
    return len(list)
img_folder_by_month = [ './img/Jan','./img/Feb','./img/Mar','./img/Apr','./img/May','./img/Jun','./img/Jul','./img/Aug','./img/Sept','./img/Oct','./img/Nov','./img/Dec']
keyword_array=['shortsleeve','longsleeve','gadigun','padding','shortshirts','court','longshirts']
month_google_link=[
    #반팔
    'https://www.google.com/search?q=%EB%82%A8%EC%9E%90+%EB%B0%98%ED%8C%94&sxsrf=APq-WBtziL3GdgSDlT1mp4AkJhizhWF0SA:1649339940032&source=lnms&tbm=isch&sa=X&ved=2ahUKEwje4vSJjoL3AhWAwosBHft3AUsQ_AUoAXoECAIQAw&biw=454&bih=560&dpr=1.5'
    #긴팔
    ,'https://www.google.com/search?q=%EB%82%A8%EC%9E%90+%EA%B8%B4%ED%8C%94&tbm=isch&ved=2ahUKEwj81LaKjoL3AhVvE6YKHZH1ClcQ2-cCegQIABAA&oq=%EB%82%A8%EC%9E%90+%EA%B8%B4%ED%8C%94&gs_lcp=CgNpbWcQAzIICAAQgAQQsQMyBQgAEIAEMgUIABCABDIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQ6BwgjEO8DECc6CwgAEIAEELEDEIMBOggIABCxAxCDAVCiBViOC2DpC2gAcAB4AIABogGIAbQHkgEDMC44mAEAoAEBqgELZ3dzLXdpei1pbWfAAQE&sclient=img&ei=Je5OYryuBu-mmAWR66u4BQ&bih=560&biw=454'
    #가디건
    ,'https://www.google.com/search?q=%EB%82%A8%EC%9E%90+%EA%B0%80%EB%94%94%EA%B1%B4&sourceid=chrome&ie=UTF-8'
    #패딩
    ,'https://www.google.com/search?q=%EB%82%A8%EC%9E%90+%ED%8C%A8%EB%94%A9&sxsrf=APq-WBuilnVR331vvSw5Ji6nBlTQnao8tw%3A1649341352680&ei=qPNOYqqAKYOc-AaTsrCQDQ&ved=0ahUKEwiq9MGrk4L3AhUDDt4KHRMZDNIQ4dUDCA4&uact=5&oq=%EB%82%A8%EC%9E%90+%ED%8C%A8%EB%94%A9&gs_lcp=Cgdnd3Mtd2l6EAMyBQgAEIAEMgUIABCABDIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQyBQgAEIAEOgcIABBHELADOgQIIxAnOgsIABCABBCxAxCDAToECAAQQzoICAAQgAQQsQM6BwgjELECECc6BAgAEAo6BAgAEA06CQghEAoQoAEQKjoHCCEQChCgAUoECEEYAEoECEYYAFCDB1jlHGD4HWgGcAF4AoABjwKIAfkSkgEFMC44LjWYAQCgAQHIAQrAAQE&sclient=gws-wiz'
    #남자 반팔 셔츠
    ,'https://www.google.com/search?q=%EB%82%A8%EC%9E%90+%EB%B0%98%ED%8C%94+%EC%85%94%EC%B8%A0&sxsrf=APq-WBu0PVAZ46SF_ckvN7Z8XYzDmpK4TQ%3A1649341362527&ei=svNOYpvmH7yl1e8PjJuH4AU&ved=0ahUKEwibh5uwk4L3AhW8UvUHHYzNAVwQ4dUDCA4&uact=5&oq=%EB%82%A8%EC%9E%90+%EB%B0%98%ED%8C%94+%EC%85%94%EC%B8%A0&gs_lcp=Cgdnd3Mtd2l6EAMyBQgAEIAEMgUIABCABDIECAAQHjIECAAQHjIECAAQHjIGCAAQCBAeMgYIABAIEB4yBggAEAgQHjoHCAAQRxCwAzoECCMQJzoLCAAQgAQQsQMQgwE6EAgAEIAEEIcCELEDEIMBEBRKBAhBGABKBAhGGABQuwVY7RFgghNoAXABeAGAAYEBiAHQDJIBBDAuMTOYAQCgAQHIAQrAAQE&sclient=gws-wiz'
    #코트
    ,'https://www.google.com/search?q=%EB%82%A8%EC%9E%90+%EC%BD%94%ED%8A%B8&sxsrf=APq-WBvHnWuT1f1QyRkXuR5TVLjgVHgPWg%3A1649341372490&ei=vPNOYovUHfmD1e8PqJaD-Ac&ved=0ahUKEwiLovu0k4L3AhX5QfUHHSjLAH8Q4dUDCA4&uact=5&oq=%EB%82%A8%EC%9E%90+%EC%BD%94%ED%8A%B8&gs_lcp=Cgdnd3Mtd2l6EAMyBQgAEIAEMgUIABCABDIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQyBQgAEIAEOgcIABBHELADOgQIIxAnOgsIABCABBCxAxCDAToQCAAQgAQQhwIQsQMQgwEQFEoECEEYAEoECEYYAFD5BVj-D2CVEWgBcAF4AIABiQGIAeIIkgEDMC45mAEAoAEByAEJwAEB&sclient=gws-wiz'
    #긴 셔츠
    ,'https://www.google.com/search?q=%EB%82%A8%EC%9E%90+%EA%B8%B4+%EC%85%94%EC%B8%A0&sxsrf=APq-WBv5OgBaGdEMhqNgiGvmOKmQ85PCVg:1649341406369&source=lnms&tbm=isch&sa=X&ved=2ahUKEwiu947Fk4L3AhVS4GEKHT03ArMQ_AUoAXoECAIQAw&biw=454&bih=560&dpr=1.5'
   
  ]

month_woman_google_link =[
    #반팔
    'https://www.google.com/search?q=%EC%97%AC%EC%9E%90+%EB%B0%98%ED%8C%94&sxsrf=APq-WBuNF_WQhOzFabhEkR5Y-fiAny4Uig:1649342653904&source=lnms&tbm=isch&sa=X&ved=2ahUKEwjwwf6XmIL3AhWSNaYKHbHVDjAQ_AUoAXoECAEQAw&biw=1234&bih=569&dpr=1.5'
    #긴팔
    ,'https://www.google.com/search?q=%EC%97%AC%EC%9E%90+%EB%B0%98%ED%8C%94&sxsrf=APq-WBuNF_WQhOzFabhEkR5Y-fiAny4Uig:1649342653904&source=lnms&tbm=isch&sa=X&ved=2ahUKEwjwwf6XmIL3AhWSNaYKHbHVDjAQ_AUoAXoECAEQAw&biw=1234&bih=569&dpr=1.5'
    #가디건
    ,'https://www.google.com/search?q=%EC%97%AC%EC%9E%90+%EA%B0%80%EB%94%94%EA%B1%B4&tbm=isch&ved=2ahUKEwjUiuOYmIL3AhWbwIsBHS7yAG4Q2-cCegQIABAA&oq=%EC%97%AC%EC%9E%90+%EA%B0%80%EB%94%94%EA%B1%B4&gs_lcp=CgNpbWcQAzIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQ6BwgjEO8DECc6CAgAEIAEELEDOggIABCxAxCDAToLCAAQgAQQsQMQgwFQtgRYvAtglQxoAnAAeAGAAZoBiAHZCZIBAzAuOZgBAKABAaoBC2d3cy13aXotaW1nwAEB&sclient=img&ei=v_hOYpSvIZuBr7wPruSD8AY&bih=569&biw=1234'
    #패딩
    ,'https://www.google.com/search?q=%EC%97%AC%EC%9E%90+%ED%8C%A8%EB%94%A9&tbm=isch&ved=2ahUKEwiho4jFmIL3AhVcSfUHHabQCTsQ2-cCegQIABAA&oq=%EC%97%AC%EC%9E%90+%ED%8C%A8%EB%94%A9&gs_lcp=CgNpbWcQAzIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQ6BwgjEO8DECc6CAgAEIAEELEDOggIABCxAxCDAVD0BFiODWDmDWgBcAB4AYABrgGIAaMHkgEDMC43mAEAoAEBqgELZ3dzLXdpei1pbWfAAQE&sclient=img&ei=HPlOYqGlGtyS1e8PpqGn2AM&bih=569&biw=1234'
    #여자 반팔 셔츠
    ,'https://www.google.com/search?q=%EC%97%AC%EC%9E%90+%EB%B0%98%ED%8C%94+%EC%85%94%EC%B8%A0&tbm=isch&ved=2ahUKEwjCz--EmYL3AhWGN5QKHfbECMIQ2-cCegQIABAA&oq=%EC%97%AC%EC%9E%90+%EB%B0%98%ED%8C%94+%EC%85%94%EC%B8%A0&gs_lcp=CgNpbWcQAzIFCAAQgAQyBQgAEIAEOgcIIxDvAxAnOgQIABAYOgYIABAHEB46BggAEAgQHjoICAAQgAQQsQM6CwgAEIAEELEDEIMBUNQOWLcdYIMfaAJwAHgBgAHTAYgB2Q6SAQYwLjEyLjGYAQCgAQGqAQtnd3Mtd2l6LWltZ8ABAQ&sclient=img&ei=ovlOYsL2Dobv0AT2iaOQDA&bih=569&biw=1234'
    #코트
    ,'https://www.google.com/search?q=%EC%97%AC%EC%9E%90+%EC%BD%94%ED%8A%B8&tbm=isch&ved=2ahUKEwiT5KSemYL3AhUMYJQKHdIKBWcQ2-cCegQIABAA&oq=%EC%97%AC%EC%9E%90+%EC%BD%94%ED%8A%B8&gs_lcp=CgNpbWcQAzIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQyBQgAEIAEMgUIABCABDIFCAAQgAQyBQgAEIAEMgUIABCABDIGCAAQCBAeOgcIIxDvAxAnOggIABCABBCxAzoICAAQsQMQgwFQ6AVYwg5gjxBoAHAAeACAAbABiAHjB5IBAzAuN5gBAKABAaoBC2d3cy13aXotaW1nwAEB&sclient=img&ei=1_lOYtOcIYzA0QTSlZS4Bg&bih=569&biw=1234'
    #긴 셔츠
    ,'https://www.google.com/search?q=%EC%97%AC%EC%9E%90+%EA%B8%B4+%EC%85%94%EC%B8%A0&tbm=isch&ved=2ahUKEwiO-qilmYL3AhXKEKYKHXvRD3sQ2-cCegQIABAA&oq=%EC%97%AC%EC%9E%90+%EA%B8%B4+%EC%85%94%EC%B8%A0&gs_lcp=CgNpbWcQAzIFCAAQgAQ6BwgjEO8DECc6BggAEAgQHjoICAAQgAQQsQM6CAgAELEDEIMBUJgFWLYNYIsOaAFwAHgBgAGTAYgB0gqSAQQwLjEwmAEAoAEBqgELZ3dzLXdpei1pbWfAAQE&sclient=img&ei=5vlOYo7vEcqhmAX7or_YBw&bih=569&biw=1234'
    ]
driver=webdriver.Chrome('chromedriver.exe')

#******setting******
pathIndex=0 #특정 이미지를 수집 할 때, 폴더 경로
linkIndex=0 #특정 검색어 이미지를 수집 할 때, 검색 경로
files = 0; #수집하고자하는 폴더에 이미지 갯수 입력
gender = 'woman' #성별 입력 
while(True):
  file_path=f'./img/{gender}/{keyword_array[pathIndex]}'
  files=get_files_count(file_path)
  print("해당 폴더의 파일 갯수는")
  print(files)
  j=0

  i = 0
  index=0   
  SCROLL_PAUASE_TIME = 3 
  driver.get(month_woman_google_link[linkIndex])
  time.sleep(3)
 
  time.sleep(2)
  while(True):
    driver.execute_script("window.scrollTo(0,window.scrollY+100);")
    time.sleep(0.1)
    try:
     image= driver.find_elements_by_css_selector('div.bRMDJf>img ')[i]
    except:
      print('index error')
      break
    url = image.get_attribute('src')
    try: 
        updateNum=files+j
        urllib.request.urlretrieve (url, f'./img/{gender}/{keyword_array[pathIndex]}/{updateNum}.jpg') 
    except: 
        break;
    print(updateNum);
    print('+');
    print(keyword_array[pathIndex])
    print('\n')
    j+=1
   
     
    print("스크롤 이벤트 발생")   
   
    i+=1
  linkIndex+=1;
  pathIndex+=1;
  print("처음 파일 갯수는")
  print(files)
  if not month_woman_google_link[linkIndex]:break
```

네이버
```c
    from distutils.log import error
from urllib.request import urlopen
from urllib.parse import quote_plus
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
import time
import os 
import urllib.request
img_folder_by_month = [ './img/Jan','./img/Feb','./img/Mar','./img/Apr','./img/May','./img/Jun','./img/Jul','./img/Aug','./img/Sept','./img/Oct','./img/Nov','./img/Dec']
keyword_array=['shortsleeve','longsleeve','gadigun','padding','shortshirts','shortshirts','court','longshirts']
month_naver_link=[
    #반팔
    'https://search.naver.com/search.naver?sm=tab_hty.top&where=image&query=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EB%B0%98%ED%8C%94+%EB%82%A8%EC%9E%90+%ED%9B%84%EA%B8%B0&oquery=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EB%B0%98%ED%8C%94+%ED%9B%84%EA%B8%B0&tqi=hCiNgwprvN8ssuqg7FCsssssscw-285182'
    #긴팔
    ,'https://search.naver.com/search.naver?sm=tab_hty.top&where=image&query=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EB%82%A8%EC%9E%90+%EA%B8%B4%ED%8C%94&oquery=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EB%82%A8%EC%9E%90+%EB%B0%98%ED%8C%94&tqi=hCjW8lp0JXVssdWRnw8ssssstQR-002936'
    #가디건
    ,'https://search.naver.com/search.naver?sm=tab_hty.top&where=image&query=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EB%82%A8%EC%9E%90+%EA%B0%80%EB%94%94%EA%B1%B4&oquery=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EB%82%A8%EC%9E%90+%EA%B8%B4%ED%8C%94&tqi=hCjyVlprvh8ssE%2F70uKssssssid-418707'
    #패딩
    ,'https://search.naver.com/search.naver?sm=tab_hty.top&where=image&query=%EB%82%A8%EC%9E%90+%ED%8C%A8%EB%94%A9&oquery=%ED%8C%A8%EB%94%A9&tqi=hCFtbdp0J14ssiwvIGCssssss58-498116'
    #남자 반팔 셔츠
    ,'https://search.naver.com/search.naver?sm=tab_hty.top&where=image&query=%EB%82%A8%EC%9E%90+%EB%B0%98%ED%8C%94+%EC%85%94%EC%B8%A0&oquery=%EB%82%A8%EC%9E%90+%ED%8C%A8%EB%94%A9&tqi=hCFt4dp0J1Zssv7miDCsssssshR-521592'
    ,'https://search.naver.com/search.naver?sm=tab_hty.top&where=image&query=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EB%82%A8%EC%9E%90+%EB%B0%98%ED%8C%94+%EC%85%94%EC%B8%A0&oquery=%EB%82%A8%EC%9E%90+%EB%B0%98%ED%8C%94+%EC%85%94%EC%B8%A0&tqi=hCFu4lp0YihssMRG0pGssssstIs-220773'
    #코트
    ,'https://search.naver.com/search.naver?sm=tab_hty.top&where=image&query=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EB%82%A8%EC%9E%90+%EC%BD%94%ED%8A%B8&oquery=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EB%82%A8%EC%9E%90+%EB%B0%98%ED%8C%94+%EC%85%94%EC%B8%A0&tqi=hCFvOlp0YiRssid6dX4ssssstO4-318190'
    ]
month_woman_naver_link =[
    #반팔
    'https://search.naver.com/search.naver?sm=tab_hty.top&where=image&query=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EC%97%AC%EC%9E%90+%EB%B0%98%ED%8C%94&oquery=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EB%82%A8%EC%9E%90+%EB%A7%A8%ED%88%AC%EB%A7%A8&tqi=hCphKwp0YidssNW2sd4ssssss6N-480276'
    #긴팔
    ,'https://search.naver.com/search.naver?sm=tab_hty.top&where=image&query=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EC%97%AC%EC%9E%90+%EA%B8%B4%ED%8C%94&oquery=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EC%97%AC%EC%9E%90+%EB%B0%98%ED%8C%94&tqi=hCphgwp0YiRssL0uLposssssswC-262966'
    #가디건
    ,'https://search.naver.com/search.naver?sm=tab_hty.top&where=image&query=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EC%97%AC%EC%9E%90+%EA%B0%80%EB%94%94%EA%B1%B4&oquery=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EC%97%AC%EC%9E%90+%EA%B8%B4%ED%8C%94&tqi=hCphpwp0JXVsshVhe0Nssssss%2F0-017592'
    #패딩
    ,'https://search.naver.com/search.naver?sm=tab_hty.top&where=image&query=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EC%97%AC%EC%9E%90+%ED%8C%A8%EB%94%A9&oquery=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EC%97%AC%EC%9E%90+%EA%B0%80%EB%94%94%EA%B1%B4&tqi=hCphqdp0JywssjEY4y4ssssssfd-262059'
    #여자 반팔 셔츠
    ,'https://search.naver.com/search.naver?sm=tab_hty.top&where=image&query=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EC%97%AC%EC%9E%90+%EB%B0%98%ED%8C%94+%EC%85%94%EC%B8%A0&oquery=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EC%97%AC%EC%9E%90+%ED%8C%A8%EB%94%A9&tqi=hCphwlp0YiRssLD1dZRssssssns-199454'
    ,'https://search.naver.com/search.naver?sm=tab_hty.top&where=image&query=%EC%97%AC%EC%9E%90+%EB%B0%98%ED%8C%94+%EC%85%94%EC%B8%A0&oquery=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EC%97%AC%EC%9E%90+%EB%B0%98%ED%8C%94+%EC%85%94%EC%B8%A0&tqi=hCphJwp0YihssuBbtlhssssstWG-384916'    
    #코트
    ,'https://search.naver.com/search.naver?sm=tab_hty.top&where=image&query=%EB%AC%B4%EC%8B%A0%EC%82%AC+%EC%97%AC%EC%9E%90+%EC%BD%94%ED%8A%B8&oquery=%EC%97%AC%EC%9E%90+%EB%B0%98%ED%8C%94+%EC%85%94%EC%B8%A0&tqi=hCpiulp0YidssN1GcXVssssstCC-382735'
     ]

driver=webdriver.Chrome('chromedriver.exe')
pathIndex=0
linkIndex=8

while(True):
 
  if linkIndex==5:
    sum=j
    j=0
  else :
    sum=401 # 존재하는 파일 갯수를 반드시 적어주어야한다.
    j=0
  i = 0
  index=0   
  SCROLL_PAUASE_TIME = 3 
  driver.get(month_naver_link[linkIndex])
  time.sleep(3)

 
  time.sleep(2)
  while(True):
    driver.execute_script("window.scrollTo(0,window.scrollY+100);")
    time.sleep(0.1)
  
    try:
     image= driver.find_elements_by_css_selector('div.thumb>a>img')[i]
    except:
      print('index error')
      break
    url = image.get_attribute('src')
    if not url=='data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7':
        updateNum=sum+j
        urllib.request.urlretrieve (url, f'./img/man/{keyword_array[pathIndex]}/{updateNum}.jpg') 
        print(updateNum)
        print(url)
        print('\n')
        j+=1
        print(i)
     
    print("스크롤 이벤트 발생")   
   
    i+=1
  linkIndex+=1;
  pathIndex+=1;
  if not month_naver_link[linkIndex]:break
  ```
  
  
## 6월 3일 발표 내용
* 수정된 주제 설명

* 모델링(티처블머신)
     
* 로그인 및 가입하기
로그인 및 가입하기 디자인 구현 부분
  ```c
  import axios from "axios";
import { useState } from "react";
import { useDispatch } from "react-redux";
import styled from "styled-components";
import { getUser } from "../../../API/login";
import FreeButton from "../../../components/CustomButton/FreeButton";
import { CustomForm, CustomInput } from "../../component/input/component";
const ModalWrap = styled.div`
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
`;

const ModalContain = styled.div`
  position: absolute;
  top: 6.5rem;
  border: 2px solid black;
  border-radius: 10px;
  z-index: 2005;
  padding: 1.5rem;
  background-color: whitesmoke;
  width: 40rem;
  @media (max-width: 1120px) {
    width: 30rem;
  }
  @media (max-width: 50rem) {
    width: 80%;
  }
  min-height: 25rem;
  animation: modal-show 1s;
  @keyframes modal-show {
    from {
      opacity: 0;
      margin-top: -50px;
    }
    to {
      opacity: 1;
      margin-top: 0;
    }
  }
`;
const ModalBack = styled.div`
  position: fixed;
  width: 100%;
  z-index: 2004;
  height: 100%;
  background-color: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(5px);
  animation: modal-bg-show 1s;
  @keyframes modal-bg-show {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
`;
const ModalBody = styled.div`
  position: relative;
  width: fit-content;
  height: 400px;
  width: 50%;
  margin: 0 auto;
  background-color: whitesmoke;
  border: 1px solid gray;
`;
const ModalHeader = styled.div`
  display: inline-block;
  position: relative;

  width: 100%;
  height: fit-content;
`;
const ModalTitle = styled.div`
  position: relative;
  width: 100%;
  background-color: #ffcce5;
  text-align: center;
`;
const ModalHeaderBtnWrap = styled.div`
  position: relative;
  left: 0;
`;
const ModalContent = styled.div`
  display: flex;
  flex-direction: column;
  justify-content: center;
`;

export default function Modal({ closeEvent, dimRef, modalState }) {
  const dispatch = useDispatch();
  const [account, setAccount] = useState({ id: "", nickname: "" });
  const [newAccount, setNewAccount] = useState({ id: "", nickname: "" });
  const [page, setPage] = useState(0);
  const next = () => {
    setPage(page + 1);
  };
  const handleChange = (e) => {
    setAccount({
      ...account,
      [e.target.name]: e.target.value,
    });
  };
  const handleNewChange = (e) => {
    setNewAccount({
      ...newAccount,
      [e.target.name]: e.target.value,
    });
  };
  const onSubmit = (e) => {
    if (account.id === "" || account.nickname === "") {
      if (account.id === "") alert("ID 혹은 비밀번호가 잘못되었습니다.");
      else if (account.nickname === "") alert("ID 혹은 닉네임 잘못되었습니다.");
    } else {
      alert("로그인");
      const result = axios
        .post(
          "http://localhost:8080/login",

          { id: account.id, nickname: account.nickname },

          {
            headers: { "Content-Type": "application/json" },
            withCredentials: "include",
          }
        )
        .then((res) => {
          console.log(res);
          setAccount({ id: "", nickname: "" });
          closeEvent();
          window.location.reload();
        })
        .catch((err) => {
          console.log(err);
        });
    }
  };
  const register = (e) => {
    if (newAccount.id === "" || newAccount.nickname === "") {
      if (newAccount.id === "") alert("ID 혹은 비밀번호가 잘못되었습니다.");
      else if (newAccount.nickname === "")
        alert("ID 혹은 닉네임 잘못되었습니다.");
    } else {
      alert("가입하기");
      const result = axios
        .post(
          "http://localhost:8080/register",

          { id: newAccount.id, nickname: newAccount.nickname },

          {
            headers: { "Content-Type": "application/json" },
          }
        )
        .then((res) => {
          setNewAccount({ id: "", nickname: "" });
          window.location.reload();
        })
        .catch((err) => {
          console.log(err);
        });
      console.log(result);
    }
  };
  return (
    <>
      {modalState && (
        <ModalBack id="modalBack" ref={dimRef}>
          <ModalWrap id="detail">
            <ModalContain id="modalContain">
              <ModalHeaderBtnWrap id="modalHeaderBtnWrap">
                <FreeButton
                  id="exitBtn"
                  text={"닫기"}
                  hoverFontColor={"red"}
                  fontSize={"15px"}
                  color={"green"}
                  clickEvent={() => {
                    setPage(0);
                    closeEvent();
                  }}
                />
              </ModalHeaderBtnWrap>
              <ModalBody id="modalBody">
                <ModalHeader id="modalHeader">
                  <ModalTitle>
                    {page === 0 && <h1>로그인</h1>}
                    {page === 1 && <h1>가입하기</h1>}
                  </ModalTitle>
                </ModalHeader>
                {page === 0 && (
                  <>
                    <ModalContent id="modalContent">
                      <CustomForm onSubmit={onSubmit}>
                        <span>아이디</span>
                        <CustomInput
                          id="ID"
                          name="id"
                          value={account.id}
                          onChange={handleChange}
                        ></CustomInput>
                        <span>닉네임</span>

                        <CustomInput
                          id="NICKNAME"
                          type="nickname"
                          name="nickname"
                          value={account.nickname}
                          onChange={handleChange}
                        ></CustomInput>
                        <FreeButton
                          hover="tictok"
                          hoverBKGColor={"pink"}
                          color={"#FFCCFF"}
                          hoverFontColor={"#FF99FF"}
                          clickEvent={() => {
                            onSubmit();
                          }}
                          text="로그인"
                        ></FreeButton>
                        <FreeButton
                          hover="tictok"
                          hoverBKGColor={"pink"}
                          color={"#FFCCFF"}
                          hoverFontColor={"#FF99FF"}
                          clickEvent={next}
                          text="가입하기"
                        ></FreeButton>
                      </CustomForm>
                    </ModalContent>
                  </>
                )}
                {page === 1 && (
                  <ModalContent id="modalContent">
                    <CustomForm onSubmit={onSubmit}>
                      <span>아이디</span>
                      <CustomInput
                        id="ID"
                        name="id"
                        value={newAccount.id}
                        onChange={handleNewChange}
                      ></CustomInput>
                      <span>닉네임</span>

                      <CustomInput
                        id="NICKNAME"
                        type="nickname"
                        name="nickname"
                        value={newAccount.nickname}
                        onChange={handleNewChange}
                      ></CustomInput>

                      <FreeButton
                        hover="tictok"
                        hoverBKGColor={"pink"}
                        color={"#FFCCFF"}
                        hoverFontColor={"#FF99FF"}
                        clickEvent={() => {
                          register();
                        }}
                        text="가입하기"
                      ></FreeButton>
                    </CustomForm>
                  </ModalContent>
                )}
              </ModalBody>
            </ModalContain>
          </ModalWrap>
        </ModalBack>
      )}
    </>
  );
}
  ```
<img width="600" alt="KakaoTalk_20220617_020755241_01" src="https://user-images.githubusercontent.com/96337129/174127613-643d3086-768c-4620-b492-db77d9e31718.png">
<img width="600" alt="KakaoTalk_20220617_020755241" src="https://user-images.githubusercontent.com/96337129/174127840-b09b8b6c-4ff0-49cf-b4e9-685ff93b09dd.png">

* 향후 계획
