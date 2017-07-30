# Signup
This is my master file code 
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Data.Sql;
using System.Data;
using System.Data.SqlClient;
using System.Text;
using System.Web.UI.HtmlControls;
using System.Web.UI.WebControls.WebParts;

public partial class signup : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {

    }
    protected void btnsignup_Click(object sender, EventArgs e)
    {
        SqlConnection Connection1 = new SqlConnection("Data Source=.;Initial Catalog=UML;Integrated Security=True");
        Connection1.Open();
        string StringCmnd1 = @"INSERT INTO [dbo].[Registration]
           ([First_Name]
           ,[Last_Name]
           ,[Email]
           ,[Password])
     VALUES
           ('" + FirstNameTextBox.Text + "','" + LastNameTextBox.Text + "','" + EmailTextBox.Text + "','" + PasswordTextBox.Text + "')";
        SqlCommand ObjCmnd1 = new SqlCommand(StringCmnd1, Connection1);
        ObjCmnd1.ExecuteNonQuery();
        Connection1.Close();
    }
}
