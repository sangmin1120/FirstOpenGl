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

#### 2024.03.07
=> F1~F6 키를 사용하여 창을 열고 화면 색상을 변경하는 함수가 구현


### 2. Hello Triangle
: 삼각형을 만들어 색을 넣었다.
=> shader는 GPU 에서 병렬처리하는 프로그램이다.
  shader 마다 입력과 출력이 필요하다. 따라서 GLSL 은 in 과 out 키워드로 출력 변수를 다음 shader에 넘겨준다.
  **1. vertex shader**
  : vertex 데이터를 곧바로 입력 받는다.
  **2. fragment shader**
  : 최종 출력 컬러를 생서하기 때문에 vec4 타입의 출력 변수가 필요하다.

  따라서 한 shader에서 다른 shader로 넘기고 싶다면 shader에서 출력을 선언해야하고 받는 shader에서 입력을 선언하면 된다.
  <u>(나중에 shader의 헤더파일을 include하여 선언할 예정이다. 아직은 코드마다 작성하였다.)</U>

  **uniform**
  : 모든 단계의 모든 shader에서 접근 가능하다. 어떤 값을 설정하든 리셋을 하거나 업데이트를 하기 전까지 그 값을 계속 유지한다.
  **VBO,VAO**
  : ??
  
