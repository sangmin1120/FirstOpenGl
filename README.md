# GPU 프로그래밍

## OpenGL
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

 * VBO는 버퍼에 저장한 vertex들을

   GPU에 올려주고 랜더링 할 때마다 다시 전송할 필요없다.
   
   버퍼 만들기 => 버퍼에 데이터 전송(바인딩) : glBindBuffer 함수로 VBO를 GL_ARRAY_BUFFER에 관해서
   
   바인딩해주면, 그 이후로 GL_ARRAY_BUFFER에 정보를 넣을 때 우리가 만들 VBO에 정보를 저장. 바인딩이 끝났으면, vertx를 VBO에 담는다.
   
   순서 : 객체 생성 --> 바인딩 --> GL_ARRAY_BUFFER에 배열 넘겨주기 --> 배열이 어떻게 해석해야 하는 지 알려주기 --> location 에 넘겨주기


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
  : VBO 하나의 정점 속성을 갖고 있는 GPU 상의 메모리 버퍼(위치 정보, 색상 등), 고유 ID를 가진다.
    1. VBO ID 준비
    2. 버퍼 객체 생성 및 ID에 바인딩
    3. 버퍼 객체 타입 바인딩
    4. 버퍼에 실질적 데이터 담기
  : VAO 하나 이상의 VBO를 담을 수 있는 객체, 고유 ID를 가진다.
    1. VAO ID 준비
    2. VAO 객체 생성 및 ID에 바인딩
    3. 객체 타입 바인딩
    
  **vertex Attribute**
  : vertex buffer에 들어가는 입력 데이터
  => glVertexAttribPointer(index,size,type,normalized,stride,pointer)
  
      index : Location 의 순서
      
      size : 정점 속성의 구성 크기(vec의 크기)
      
      type : 배열 내 데이터들의 타입
      
      normalized : 정규화되어야하는 지 여부 전달
      
      stride : 배열 내 각각 데이터의 byte offset
      
      pointer : 해당 정점 속성의 시작 byte 위치
      
  => glEnableVertexAttribArray(index) : 해당 인덱스에 위치한 정점 속성 배열을 활성화
      index : 활성화시킬 정점 속성 배열이 위치한 인덱스

  ### 3. Texture
  : 그림 2개를 가져와 겹쳐 놓는다. wrap과 minmap,filtering에 대해 알아 보았다.
  
  wraping : 텍스쳐의 설정 범위가 크기를 넘으면 어떻게 설정할 것인가. 
  
  filtering : 좌표의 색을 보간으로 할지, 그 색상에 값으로 할지 설정.

  Mipmaps : 텍셀의크기 < 픽셀의 크기 일 때 Minmap의 유사한 크기와 매칭


  => 1. 텍스처 생성 후 바인딩 , 필요시 텍스처 wrapping/filtering 설정
  
     2. 2D 텍스처 생성 및 Minmaps 생성
     ( shader에서는 'sampler2D' 변수로 입력받는다 )

     
     -벡터의 다양한 연산 방법.

  ### 4. Coordinate System

  local space => (model) => world space => (view) => view space => (projection) => slip sapce => viewport => screen space

  *local : 객체의 원점을 (0,0,0) 기준으로 놓는 공간이다. shader에 vertex를 넘겨줄 때 좌표를 생각하면 된다.

  * world : local space 상의 객체를 실제 model matrix를 이용해 이동 , 스케일 , 회전 을 한다.

  * view : Camera 의 과전에서 바라보는 공간

  * clip : NDC 좌표로 변환하여 보여준다. NDC의 범위를 벗어나면 clipping한다.

  * 직교 투영 / 원근 투영
    : 원근감을 고려하지 않음 / 원근감을 고려해서 가까이있을 수록 크게 보인다.
    
    - 증명 방법

  * 카메라 정의 : 위치 , 방향 벡터 , right vector , up vector  를 정의 해야됨 Look At 행렬에서 한 번에 정의할 수 있다.

  * deltaTime , lastframe 을 이용해 frame rate와 관계없이 균일한 속도로 이동하도록 구현.

  * 카메라의 Euler Angles 
