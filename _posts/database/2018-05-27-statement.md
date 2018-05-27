---
layout: post
title: statement
categories: database
---
# 연동 단계
1. Driver Manager : class.forName("드라이버 이름") 또는 DriverManager.registerDriver("드라이버 이름");
2. Connection : Connection conn = DriverManager.getConnection(드라이버 url, 사용자 계정, 비밀번호);
3. Statement : [Statement / PreparedStatement / CallableStatement] stmt = conn.[createStatement() / prepareStatement() / prepareCall()];
4. execute  : stmt.[execute() / exucuteQuery() / executeUpdate()];
---
# Statement
디폴트 : 읽기와 forward
 + 스크롤 여부에 따라
    - TYPE_FORWARD_ONLY
    - TYPE_SCROLL_INSENSITIVE : 변경 신경 X
    - TYPE_SCROLL_SENSITIVE  : 변경 신경 O
 + ResultSet에 수정 가능 여부 (Concurrency option)
    - CONCUR_READ_ONLY
    - CONCUR_UPDATABLE

{% highlight java %}
  Statement stmt = conn.createStatement(TYPE 옵션)
 // Execute
  boolean stmt.execute(sql);
  ResultSet stmt.exucuteQuery(sql);
  ResultSet stmt.executeUpdate(sql);
 {% endlight java %}


# PreparedStatement
{% highlight java %}
PreparedStatement pstmt = conn.prepareStatement(?가 포함된 sql문);
pstmt.setINT(1, value); // 인덱스는 1부터
pstmt.executeQuery();
{% endlight java %}

---
# ResutlSet = 질의 결과에 대한 Object(Cursor)
{% highlight java %}

ResutlSet rs = stmt.exucuteQuery(sql);
rs.next(); // 다음 row 이동
rs.moveToInsertRow();
rs.moveToCurrentRow();
rs.delete();
rs.absolute();
rs.updateString();
rs.getString([칼럼이름 / 칼럼번호]);

{% endlight java %}
