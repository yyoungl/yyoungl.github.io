---
layout: default
title: JAVA I/O Stream, Serialization
nav_order: 111
description: JAVA I/O Stream, Serialization
parent: Java
---

# 230728 I/O와 Stream, Serialization

pdf: 230728%20I%20O%E1%84%8B%E1%85%AA%20Stream,%20Serialization%2040e55b7bb92543589fc0412d0813afa8/10%25EA%25B8%25B0\_%25EC%259E%2590%25EB%25B0%2594%25EB%25B9%2584%25EC%25A0%2584%25EA%25B3%25B5_Java_day10_0728.pdf
생성 일시: 2023년 7월 28일 오전 8:48

- I/O와 Stream
- 보조 스트림
- 객체 직렬화

# I/O Stream

---

## I/O

- 데이터의 입력 (Input) / 출력 (Output)
- 컴퓨터 내부 혹은 외부의 장치와 데이터를 주고받는 행위

## Stream

- 데이터를 운반하는 데 사용되는 통로
- 물흐름과 같이 단방향으로만 통신 가능
- 하나의 스트림을 이용하여 입력과 출력 처리 불가능

![Untitled](230728%20I%20O%E1%84%8B%E1%85%AA%20Stream,%20Serialization%2040e55b7bb92543589fc0412d0813afa8/Untitled.png)

## Stream 종류

![Untitled](230728%20I%20O%E1%84%8B%E1%85%AA%20Stream,%20Serialization%2040e55b7bb92543589fc0412d0813afa8/Untitled%201.png)

## 바이트 스트림 (byte stream)

- 바이트 단위로 출력
- 주로 이진데이터를 읽고 쓰기 위해 사용

![Untitled](230728%20I%20O%E1%84%8B%E1%85%AA%20Stream,%20Serialization%2040e55b7bb92543589fc0412d0813afa8/Untitled%202.png)

- **Input Stream**
  | 메서드 명                                      | 선언부와 설명                                                                        |
  | ---------------------------------------------- | ------------------------------------------------------------------------------------ |
  | public abstract int read()                     | byte 하나를 읽어서 int로 반환한다                                                    |
  | 더 이상 읽을 값이 없으면 -1을 리턴한다         |
  | public int read(byte b[])                      | 데이터를 읽어서 b를 채우고 읽은 바이트의 개수를 리턴한다                             |
  | public int read(byte b[], int offset, int len) | 최대 len만큼 데이터를 읽어서 b의 offset부터 b에 저장하고 읽은 바이트 개수를 리턴한다 |
  | public void close()                            | 스트림을 종료해서 자원을 반납한다                                                    |

## 문자 스트림 (character stream)

- 문자 단위로 주고받을 때
- **Reader**
  | 메서드 명                                            | 선언부와 설명                                                                         |
  | ---------------------------------------------------- | ------------------------------------------------------------------------------------- |
  | public int read()                                    | 문자 하나를 읽어서 int로 반환한다                                                     |
  | 더 이상 읽을 값이 없으면 -1을 리턴한다               |
  | public int read(char[] c)                            | 데이터를 읽어서 배열 c를 채우고 읽어온 개수 또는 -1을 반환한다                        |
  | abstract public int read(char[] c, int off, int len) | 최대 len만큼 데이터를 읽어서 배열 c의 off 위치부터 저장하고 읽은 char 개수를 리턴한다 |
  | public int read(CharBuffer target)                   | 데이터를 읽어서 target에 저장한다                                                     |
  | public void close()                                  | 스트림을 종료해서 자원을 반납한다                                                     |
- **Writer**
  | 메서드 명                                              | 선언부와 설명                                                      |
  | ------------------------------------------------------ | ------------------------------------------------------------------ |
  | public void write(int b)                               | b의 내용을 char로 출력한다                                         |
  | public void write(char[] c)                            | 주어진 배열 c에 저장된 모든 내용을 출력한다                        |
  | abstract public void write(char[] c, int off, int len) | 주어진 배열 c에 저장된 내용 중에서 off부터 len 길이만큼만 출력한다 |
  | public void write(Strgin str)                          | 주어진 문자열 str을 출력한다                                       |
  | public void write(String str, int off, int len)        | 주어진 문자열의 일부를 출력한다                                    |
  | abstract public void flush()                           | 버퍼가 있는 스트림에서 버퍼의 내용을 출력하고 버퍼를 비운다        |
  | abstract public void close()                           | 스트림을 종료해서 자원을 반납한다                                  |
  | close()는 내부적으로 flush()를 호출한다                |

## File

- 가장 기본적인 입출력 장치 중 하나로 파일과 디렉터리를 다루는 클래스
  ![Untitled](230728%20I%20O%E1%84%8B%E1%85%AA%20Stream,%20Serialization%2040e55b7bb92543589fc0412d0813afa8/Untitled%203.png)
  ![Untitled](230728%20I%20O%E1%84%8B%E1%85%AA%20Stream,%20Serialization%2040e55b7bb92543589fc0412d0813afa8/Untitled%204.png)

# 보조 스트림

---

## 보조 스트림

- 스트림의 기능을 보완하기 위해 사용
- 실제 데이터를 주고받는 스트림이 아니므로 보조 스트림만으로 입출력 불가
- 스트림 생성 후 보조스트림 생성하여 사용 가능
- 여러 보조 스트림을 연결하여 사용 가능
  ```java
  new BufferedInputStream(System.in);
  new DataInputStream(new BufferedInputStream(new FileInputStream());
  ```
- 보조 스트림의 `close()`를 호출하면 노드 스트림의 `close()`까지 호출됨

### 보조 스트림의 종류

![Untitled](230728%20I%20O%E1%84%8B%E1%85%AA%20Stream,%20Serialization%2040e55b7bb92543589fc0412d0813afa8/Untitled%205.png)

![Untitled](230728%20I%20O%E1%84%8B%E1%85%AA%20Stream,%20Serialization%2040e55b7bb92543589fc0412d0813afa8/Untitled%206.png)

Buffered vs Scanner

Scanner 권장!

# 객체 직렬화

---

## 직렬화 (serialization)

- 객체가 가진 데이터를 순차적인 형태로 변환하는 절차: 데이터를 원활히 주고받기 위해
- 객체를 데이터 스트림으로 만드는 것
- 반대의 경우 역직렬화 (deserialization)
  ![Untitled](230728%20I%20O%E1%84%8B%E1%85%AA%20Stream,%20Serialization%2040e55b7bb92543589fc0412d0813afa8/Untitled%207.png)

### 직렬화 (serialization) 가능 클래스 만들기

- Serializable 인터페이스 구현 (내용은 x)
- 해당 인터페이스를 구현한 클래스를 상속받았다면 구현하지 않아도 된다
- 자손에만 구현했다면 조상클래스의 인스턴스 변수는 직렬화 대상에서제외된다
- transient 키워드를 통해 직렬화 대상에서 제외시킬 수 있다

### serialVersinUID

- 직렬화된 객체를 역직렬화할때는 직렬화 했을 때와 같은 클래스를 사용해야 한다
- 따라서 해당 UID를 활용하여 클래스의 변경 여부를 파악한다
- 작성하지 않으면 컴파일러가 자동으로 생성 (멤버 변경 시 자동 수정 → 위험)
- 따라서 작성하는 것을 권장
  ```java
  public class Person implements Serializable {
  	private static final long serialVersionUID = 1L; //임시
  	private String name;
  	private int age;
  	...
  }
  ```

### 7/31 월말 평가 안내

- 3문제 문법 문제
- 1문제 클래스 다이어그램 보고 구현하는 문제
- 워크스페이스 폴더를 압축하여 제출
- 스캐너 입력 or 변수 선언: 상관없음
- 난이도 있는 방식으로 한다면 보너스 점수 주는 문제 있음
- 조건문, 반복문, 1차원 배열
- 싱글톤 패턴 구현
- 주석으로 설명해야 됨 (없거나 미흡하면 감점)
