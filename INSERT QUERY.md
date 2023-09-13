

```java
package com.ssafy.jdbc_test;

import java.sql.*;

public class InsertTest {
	
	public InsertTest() {
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			System.out.println("Drivate Loading Success !!!!!");
		} catch (ClassNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
	
	public static void main(String[] args) {
		InsertTest it = new InsertTest();
		
		String id = "kimsw";
		String name = "승우";
		String pwd = "1234";
		
		int cnt = it.register(id, name, pwd);
		// 나중에 메서드는 외부 클래스에 빼야 함!, Main, Model, DAO, SERVICE etc..
		if(cnt != 0) {
			System.out.println("회원가입 성공!");
		} else {
			System.out.println("회원가입 실패!");
		}
	}

	private int register(String id, String name, String pwd) {
		int cnt = 0;
		Connection conn = null;
		Statement stmt = null;
		
		try {
			conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/ssafy_db?serverTimezone=UTC", "ssafy", "ssafy");
			System.out.println("DB 연결 성공!");
			StringBuilder sql = new StringBuilder("insert into ssafy_member (userid, username, userpwd) \n");
			sql.append("values ('"+ id + "', '" + name + "', '" + pwd +  "')");
			stmt = conn.createStatement();
			cnt = stmt.executeUpdate(sql.toString());
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} finally {
			try {
				if(stmt != null) { // Prevent to NPE
					stmt.close();
				}
				if(conn != null) {
					conn.close();	
				}
			} catch (SQLException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}
		
		return cnt;
	}
}


```

