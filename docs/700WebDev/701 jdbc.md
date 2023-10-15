---
layout: default
title: Java Project 와 SQL Database 연결하기 - JDBC (Java DataBase Connectivity) 활용, MySQL
nav_order: 701
parent: Web Dev
---

# Java Project 와 SQL Database 연결하기 - JDBC (Java DataBase Connectivity) 활용, MySQL

## **Java Project - MySQL 연결: Java DataBase Connectivity**

수업에서 MySQL을 활용한 데이터베이스 관리 방법을 배웠다. Java 프로젝트와 MySQL로 구축한 데이터베이스를 연결해 보자!

프로젝트에서 MySQL을 연결하려면, 초기 설정이 필요하다. 한번 살펴보자!

### **다운로드받기**

[MySQL :: Download Connector/J](https://dev.mysql.com/downloads/connector/j/)

MySQL 사이트에 들어가면 관련 .jar 파일을 받을 수 있다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrTwEm%2FbtsytRCCvPk%2FaPohD9qpl5ODxDBKbkKYtK%2Fimg.png)

여기서 두 번째 파일을 받아 압축을 푼 후, .jar 파일을 프로젝트 내 라이브러리 폴더 lib에 담으면 된다.

java src 폴더 내에 있는 DBUtil을 완성해 주면 된다.

### **DBUtil 클래스 완성하기**

정확히 말하면, DBUtil 클래스는 인스턴스를 제공하고, DB 연결이 완료되었을 때 없애는 작업만 한다.

SQL문을 작성하고, 결과를 다루는 부분은 Dao 파트에서 한다. 오늘은 개발 환경 구축 시 DB 연결과 연결 해제만 정리해 보았다.

연결할 데이터베이스의 url과 이름을 설정한다. 편리한 유지보수를 위해 final 변수를 활용하여 선언하고, 적용하자!

#### **DB 연결 및 DBUtil 싱글톤 구현**

DriverManager는 기본적으로 제공되는 클래스이고, 여기서 Connection을 가져온 다음, Connection으로 PreparedStatement를 통해 ResultSet을 가져온다. 따라서 생성 순서도 DriverManager -> Connection -> PreparedStatement -> ResultSet 순이다.

```java
// DB와 연결하기위해 필요한 DB의 URL
private final String url = "jdbc:mysql://localhost:3306/dburl입력";
// DB의 USER 이름
private final String username = "id";
// 위 USER의 PASSWORD
private final String password = "password";
// Mysql 드라이버 클래스 이름
private final String drivername = "com.mysql.cj.jdbc.Driver";
private static DBUtil instance = new DBUtil();

private DBUtil() {
	try {
		Class.forName(drivername);
	} catch (ClassNotFoundException e) {
		e.printStackTrace();
	}
}

public static DBUtil getInstance() {
	return instance;
}
	public Connection getConnection() throws SQLException {
	return DriverManager.getConnection(url, username, password);
}
```

제거 순서는 반대로 해야 한다. ResultSet -> PreparedStatement -> Connection 순이다.

```java
// 자원 해제
public static void close(Connection conn, PreparedStatement pstmt) {
	try {
		if (pstmt != null)
				pstmt.close();
		} catch (SQLException e) {
		// TODO Auto-generated catch block
			e.printStackTrace();
		}
	try {
		if (conn != null)
			conn.close();
	} catch (SQLException e) {
		// TODO Auto-generated catch block
		e.printStackTrace();
	}
}
public static void close(Connection conn, PreparedStatement pstmt, ResultSet rs) {
	try {
		if (rs != null)
			rs.close();
	} catch (SQLException e) {
		// TODO Auto-generated catch block
		e.printStackTrace();
	}
	try {
		if (pstmt != null)
			pstmt.close();
	} catch (SQLException e) {
		// TODO Auto-generated catch block
		e.printStackTrace();
	}
	try {
		if (conn != null)
			conn.close();
	} catch (SQLException e) {
		// TODO Auto-generated catch block
		e.printStackTrace();
	}
}
```
