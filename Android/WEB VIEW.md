#Android

### 참고자료
[웹뷰는 왜 사용하는가 ? ](https://docs.tosspayments.com/common/glossary/webview)


# 웹 뷰 

웹뷰(WebView)는 **네이티브 앱에 내재되어 있는 웹 브라우저입니다.** 웹뷰를 사용하면 웹 콘텐츠를 네이티브 앱 뷰와 같이 사용자에게 보여줄 수 있어요. 일반 웹 브라우저와 달리 웹뷰에는 주소창, 새로고침, 즐겨찾기와 같은 기능은 없고 단순히 웹페이지만 보여줘요.
# 웹뷰의 사용 이유

기술적인 한계. 

APP 내에서 결제 모듈을 이용하는 경우가 많음. 이런 경우 WebView를 끌어다가 사용하는 경우가 많다. 결제 모듈을 APP으로 개발하기에는 너무나도 시간이 많이 걸리고 구현하기가 어렵기 때문이다. 

PG사에서 구현해놓은 결제 모듈과 API를 가져다 사용하면 간단한 일을, 굳이 새로 만들 필요는 없다. 