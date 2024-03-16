### OpenGL
: GPU를 사용하는 블루프린트와 같은 것

### GLFW
: 창을 열거나 컨텍스트를 생성하거나 표면을 처리하거나 입력을 받는 데 사용됨

### GLAD
: 흩어진 함수를 찾고 함수 포인터를 검색하는 데 도움이 됨

### 1. Hello window
: window 창을 생성.(main 함수의 동작하는 순서와 함수 설명)
  1. glfwInit : GLFW를 초기화
  2. glfwWindowHint : GLFW를 설정 => GLFW 접두어로 옵션 선택
  3. GLFW* window = glfwCreateWindow(height,width,'창 이름',null,null)

  // GLAD 초기화<br>
  // OpenGl에게 렌더링 윈도우 사이즈 알려줘야됨.
  1. glviewport(0,0,height,width) => 첫 번째, 두 번째 인자는 윈도우의 왼쪽 아래 모서리 설정

  // while 루프에서 렌더링
  1. processInput(window) // glfwGetkey(window,   ) 로 확인하는 함수 만듬

  // 렌더링
  glcearColor(0.2f,0.3f,0.3f,1.0f)
  glClear(GLCOLOR_BUFFER_BIT) => 버퍼 비트 전달해 색을 지정

  // 이벤트를 확인하고 버퍼를 교체
  glfwSwapBuffers(window) => 컬러 버퍼(GLFW 창 안의 각 픽셀들에 대한 컬러값을 가지고 있는 버퍼)를 교체
  glfwPollEvents() => 키보드 입력, 마우스 이동 이벤트 발생했는 지 확인

## 2024.03.07
=> F1~F6 키를 사용하여 창을 열고 화면 색상을 변경하는 함수가 구현되었습니다.
1. GLFWwindow를 사용하여 창 객체가 생성되었습니다.
2. 뷰포트 설정 (?): 렌더링할 창을 가리킵니다.
3. 입력: processInput 함수가 구현되었습니다. Esc를 눌러 종료하고 F1에서 F6까지의 키 입력을 확인합니다.
