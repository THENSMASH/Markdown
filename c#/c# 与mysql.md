# c# 与mysql

```c#
    ​     using System;
    ​  using System.Collections.Generic;
    ​  using System.Data;
    ​  using System.Drawing;
    ​  using System.Linq;
    ​  using System.Text;
    ​  using System.Threading.Tasks;
    ​  using System.Windows.Forms;
    ​  using MySql.Data.MySqlClient;**//自己导入的mysql.data.dll已经下载好在c盘另外**
    ​  using System.Configuration;**//这个也是额外添加的**

​     namespace selection
​     {
​         public partial class UserRegisterForm : Form
​        {
​        //String connetStr = "server=127.0.0.1;port=3306;user=root;password=root;database=userinfo";
​        protected static MySqlConnection conn = new MySqlConnection();**//按照地址，找到C#与MySQL连接的通道（只是找到了连接通道，并未打开）**
​        protected static MySqlCommand comm = new MySqlCommand();
​        private static string connectionString = ConfigurationManager.ConnectionStrings["connString"].ConnectionString;



​  **//使用 ConfigurationManager 来读取一些常量。如链接数据库字符串**

    public UserRegisterForm()
        {
            InitializeComponent();
        }


```c#
 public static int ExecuteNonQuery(string sql, CommandType CmdType, params MySqlParameter[] splist)
   //ExecuteNonQuery 执行一些 增删改
    {
        using (MySqlConnection connection = new MySqlConnection(connectionString))//用现有的数据库连接执行一个sql命令（不返回数据集）//链接字符串：对我们的连接进行设置的字符串
        {
            connection.Open();//打开数据库
            using (MySqlCommand cmd = new MySqlCommand(sql, connection))
            {
                cmd.CommandType = CmdType;//命令类型（存储过程，文本等等）
                if (splist.Length > 0)
                {
                    cmd.Parameters.AddRange(splist);//将MySqlParameter[]数组添加到参数里，没有参数可以不写
                }
                return cmd.ExecuteNonQuery();//对于Update、insert、Delete语句执行成功是返回值为该命令所影响的行数
                                             //如果影响的行数是0，则返回值就是0
                                             // 对于所有其他类型的语句，返回值为 - 1如果发生回滚，返回值也为-1；
                                             //我们一般对于更新操作，通过判断返回值是否大于0，这个是没有问题的。
                                             //但是对于其他的操作【如对数据结构的操作（建表等）】如果操作成功返回值却是 - 1，
                                             //但是要注意一下啊，例如给数据库添加一个新表，创建成功返回 - 1，
                                             //如果操作失败就会发生异常，所有执行这种操作最好用Try,Catch语句来捕捉异常。
                                             //二、 command对象通过ExecuteNonQuery方法更新数据库的过程非常简单，步骤如下：

                //  1.创建数据库连接；

                //2.创建Command对象，并指定一个SQL Inser、Update、Delete查询或者存储过程；

                //3.把Command对象依附到数据库连接上；

                //4.调用ExecuteNonQuery()方法；

                //5.关闭连接。
            }
        }
    }
    public int Add(string Name,string Password,string Post)
    {
        string sql = "insert into UserInfo(NAME,PASSWORD,POST) values(@NAME,@PASSWORD,@POST)";
        MySqlParameter spName = new MySqlParameter("@NAME", MySqlDbType.VarChar) { Value = Name };//传参数
        MySqlParameter spPassword = new MySqlParameter("@PASSWORD", MySqlDbType.VarChar) { Value = Password };
        MySqlParameter spPost = new MySqlParameter("@POST", MySqlDbType.VarChar) { Value = Post };
        return ExecuteNonQuery(sql, CommandType.Text, spName, spPassword, spPost);

    }
    public bool Register(string Name,string Password,string Post)
    {
        return Add(Name, Password, Post) > 0;
    }
    private void RegisterEnter_Click(object sender, EventArgs e)
    {
        if((NameT.Text == "")||(PasswordT.Text =="")||(CheckPasswordT.Text == "")||(PostT.Text == ""))
        {
            MessageBox.Show("文本框不能为空！");
        }
        else
        {
            if(PasswordT.Text == CheckPasswordT.Text)
            {
                string NAME = NameT.Text;
                string PASSWORD = PasswordT.Text;
                string POST = PostT.Text;
                if(Register(NAME,PASSWORD,POST))
                {
                    MessageBox.Show("添加成功！");
                }
            }
            else
            {
                MessageBox.Show("确定密码不一样！");
            }
        }
    }

    private void back_Click(object sender, EventArgs e)
    {
        this.Hide();
        UserManagementForm f4 = new UserManagementForm();
        f4.StartPosition = FormStartPosition.CenterScreen;
        f4.Show();
    }

    private void NewUserRegister_FormClosing(object sender, FormClosingEventArgs e)
    {
        DialogResult dr = MessageBox.Show("是否退出？", "提示：", MessageBoxButtons.OKCancel, MessageBoxIcon.Information);
        //?
        if (dr == DialogResult.OK)     //如果单击“是”按键
        {
            Environment.Exit(0);

            e.Cancel = false;           //关闭窗体
        }
        else if(dr == DialogResult.Cancel)
        {
            e.Cancel = true;            //不执行操作
        }
    }

    private void NewUserRegister_Load(object sender, EventArgs e)
    {
        PostT.Items.Add("管理员");
        PostT.Items.Add("操作员");
    }
}
```

}

## SqlCommand类型

**SqlConnection** 连接

**SqlCommand** : sql命令封装

注意：**只要用到ip地址就要开TCP/IP协议**

MySqlConnection connection = new MySqlConnection(connectionString)；**//根据字符串创建了一个来连接对象**

MySqlCommand cmd = new MySqlCommand(sql, connection)； **//创建一个sql命令对象**

cmd.Connnection = conn;**//给命令对象 指定连接对象**，因为要知道连接到哪个数据库

connection.open();**//一点要在执行命令前打开**

cmd.CommandText = “Insert into”;**//放sql脚本** 换行则添加@

cmd.ExecuteNonQuery();**//执行一个非查询sql语句，返回受影响的行数**

conn.Close();**不要忘记关闭数据库**

show **优美的写法**

about **语法的简便写法**

 using (MySqlConnection connection = new MySqlConnection(connectionString))

{

connection.open()；

 using (MySqlCommand cmd = new MySqlCommand(sql, connection))

{

}

}

## 5.SQL用户注入

——登入窗体破解

——配置文件

​  ————首先在app.config文件中添加 节点，如下：

​

```c#
<connectionStrings>
<add name="connString" connectionString="server=127.0.0.1;port=3306;user=root;password=root;database=userinfo"/></connectionStrings>
```

————在项目中添加System.Configuration程序集引用（控制台和winform才需要）

————在项目中使用ConfigurationManager获取链接字符串

————列如

```c#
private static string connectionString = 
    ConfigurationManager.ConnectionStrings["connString配置名"].ConnectionString;
```

——ExecuteScalar()**返回第一行第一列的值**
