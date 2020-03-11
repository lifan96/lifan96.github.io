---
title: Session之验证码案例
date: 2020-02-04 13:47:13
categories: Java
---

## 案例需求

 	1. 访问带有验证码的登录页面login.jsp
 	2. 用户输入用户名，密码以及验证码。
     * 如果用户名和密码输入有误，跳转登录页面，提示:用户名或密码错误
     * 如果验证码输入有误，跳转登录页面，提示：验证码错误
     * 如果全部输入正确，则跳转到主页success.jsp，显示：用户名,欢迎您

![image](https://tva4.sinaimg.cn/large/80ceacb8ly1gbkboox5mcj211s0h8gmj.jpg)

##  代码实现

```java
@WebServlet("/loginServlet")
public class LoginServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1.设置编码
        request.setCharacterEncoding("utf-8");
        //2.获取参数
        String username = request.getParameter("username");
        String password = request.getParameter("password");
        String checkCode = request.getParameter("checkCode");

        //先获取服务器生成的验证码
        HttpSession session = request.getSession();
        String checkCode_session = (String) session.getAttribute("checkCode_session");

        //删除session中的存储验证码
        session.removeAttribute("checkCode_session");

        //3.先判断验证码是否正确
        if (checkCode_session != null && checkCode_session.equalsIgnoreCase(checkCode)){
            //忽略大小写比较
            //验证码正确
            //判断用户名和密码是否一致
            if ("zhangsan".equals(username) && "123".equals(password)){
                //登录成功
                //存储信息，用户信息
                session.setAttribute("user",username);

                //重定向到success.jsp
                response.sendRedirect(request.getContextPath()+"/success.jsp");

            }else {
                //登陆失败
                //存储提示信息到request
                request.setAttribute("login_error","用户名或密码错误！");
                //转发到登录页面
                request.getRequestDispatcher("/login.jsp").forward(request,response);

            }

        }else {
            //验证码不一致
            //存储提示信息到request
            request.setAttribute("cc_error","验证码错误！");
            //转发到登录页面
            request.getRequestDispatcher("/login.jsp").forward(request,response);
        }


    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request, response);
    }
}
```



