# 발표 스크립트

안녕하세요 저는 9조 발표를 맡은 서창연입니다.
지금부터 저희 9조가 개발할 AI 기술을 활용한 학습 도우미 앱을 소개하겠습니다.

----------
목차는 지금까지 다른 발표자분들과 비슷하게 다음과 같고요.

----------
먼저 소개입니다.
모두 아시다시피 이번 팀 프로젝트의 주제는 캠퍼스 라이프에 도움이 되는 소프트웨어 만들기입니다. 이번 챕터에서는 어떤 고민을 통해 학습 도우미 앱이라는 주제를 선택했는지, 달성하고자 하는 목표가 무엇인지 위주로 설명드리겠습니다.

----------
대학생이 되고 나서 가장 놀랐던 점은, 생각보다 공부를 위한 자료가 많지 않다는 것이었습니다. 전공 교과서의 연습문제는 적고, 그나마도 답안지 별첨에 가격도 사악해서 구매할 엄두가 나지 않았었죠.
그래서 수업을 듣고 이해한 내용을 정확히 알고 있는지 점검 하기가 어려웠습니다. 친구와 서로서로 각자 알고 있는것이 맞는지 물어가면서 밤을 샜던 적이 많은것 같아요.
그나마 군대를 갔다온 뒤엔 ChatGPT의 등장으로 친구 대신 지피티에게 물어볼 수 있게 되었지만, 그것도 결국 내 필요에 맞는 학습 도움을 받기엔 한계가 있었습니다.
이런 고민 끝에 저희는 LLM을 학업에 쉽게 이용할 수 있는 학습 도우미 챗봇을 개발하기로 결정했습니다.

----------
기존 솔루션들은 부분적으로 학습 도움 기능을 지원하고 있으나, 학생의 입장에서 가장 필요한 강의 교안 요약기능, 연습문제 생성 기능은 없었습니다. 커뮤니티 에브리타임 에서는 질문-답변의 형태로 학업에 도움을 받을 수 있었지만, 커뮤니티에 치중된 앱 특성상 학업에 필요한 기능이 부족했습니다.

----------
이에 저희는 학업 관련 질의응답이 가능함과 동시에, 연습 문제 생성이 가능한 학습 도우미 챗봇 쓱터디를 개발하기로 했습니다.

----------
다음은 세부 구현 계획입니다.

----------
필수 기능은 챗봇과 질문답변 커뮤니티 공간인데요, 그 중 챗봇 먼저 소개하겠습니다.
보시다시피 일반적인 채팅방의 UI를 갖고 있구요, 사용자는 채팅과 이미지를 입력할 수 있습니다.
일반적으로 이미지는 사용자가 직접 촬영한 교안 이미지가 되겠죠

----------
위 입력을 기반으로 사용자는 추가적인 요청을 할 수 있습니다. 챗봇은 맥락을 고려하여 뒤따르는 요청에 대한 설명을 해줍니다. 이 때 LANGCHAIN 기술을 사용합니다.

----------
사용자가 이미지를 입력한 경우, OCR 을 통해 이미지에서 텍스트를 인식하고, 이를 바탕으로 챗봇에게 요약 등의 액션을 요청할 수 있습니다.

----------
저희 앱의 핵심 기능으로, 사용자가 지금까지 입력한 강의 및 수업 관련 정보를 바탕으로 연습 문제를 생성할 수 있습니다. GPT API 및 기타 연습문제 데이터셋을 활용한 자체 모델을 사용해 고품질의 연습문제를 생성하고, 이를 텍스트 혹은 이미지의 형태로 사용자에게 보여줍니다.

----------
다음은 학습 커뮤니티 기능인데요, 과목별로 구분된 별개의 공간에서 질문을 주고 받을 수 있는 방식을 고려중입니다. 챗봇 기능과의 적절한 통합을 통해, 챗봇이 생성한 연습문제를 앱 내에서 풀고, 궁금한 점이 있으면 질문 게시판으로 연동시키는 방식으로의 확장을 고려중입니다.

----------
세부 구현 계획은 다음과 같습니다.
백엔드는 서버 프레임워크로 파이썬 Flask를 사용할 것입니다. DBMS 로는 MariaDB를 사용합니다. 백엔드 및 db는 aws ec2 및 s3에 배포됩니다.
AI 모델 학습은 pytorch를 사용합니다. 백엔드와 마찬가지로 배포는 aws에 할 예정입니다.
프론트엔드는 우선 android 앱으로 개발할 예정이며 kotlin을 사용합니다. 선언형 UI 프레임워크인 Compose를 사용하여 추후 동일 코드로 iOS와 Desktop 앱으로 확장할 계획입니다.

----------
다음은 역할 분배입니다
저희 팀 구성원은 총 7인으로, 프론트엔드에 3명, 백엔드 3명, AI 1명으로 구성했습니다. 각 파트별 세부 업무 분배는 슬라이드를 참조해 주세요.

----------
다음은 프로젝트 일정입니다
오늘 발표 이후로 2주동안 UI/UX 디자인을 진행하고, 요구사항을 정의한 뒤 이에 맞는 API 명세를 작성할 예정입니다.
백엔드와 AI에서는 DB 스키마를 설계하고, GPT API가 연동된 langchain 모델 개발을 시작할 예정입니다.
이후 2주간은 UX 구현을 진행하고, 서버 내부로직 구현 및 OCR 엔진을 개발합니다.
10~11주차는 api를 연동하고, happy case에 대한 핑거 테스트, 코드 기반 단위 테스트 및 데모버전 앱 빌드를 진행합니다.
마지막 2주차는 QA주차로, 2주간 통합 테스트 및 수정을 진행합니다. 최종 버전의 앱을 발행하고, 스토어에 업로드한 뒤 최종 발표를 준비합니다.

----------
마지막으로 기대효과입니다

----------
첫번째로 OCR과 GPT를 활용해 필요한 지식을 빠르게 학습하고, 점검할 수 있습니다.
두 번째로 챗봇과 상호작용하는 UX로 개별 사용자의 니즈에 적합한 학습 도움을 줄 수 있습니다.
마지막으로 교과목별 커뮤니티를 형성해 챗봇으로 생성한 다양한 학습 자료를 다른 학우들과 공유할 수 있습니다.
궁극적으로 일련의 기능을 활용해 이 서비스의 주 이용자인 성균관대 학생들의 학업능력 향상에 기여할 수 있습니다.

----------

발표는 여기까지입니다.
