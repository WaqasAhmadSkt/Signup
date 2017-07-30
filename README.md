# Signup
This is my branch file code 
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
    private Boolean userExist;
    protected void Page_Load(object sender, EventArgs e)
    {

    }
    protected void btnsignup_Click(object sender, EventArgs e)
    {
        checkUserExist();
        if (userExist == false)
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
            ShowAlert();
            FirstNameTextBox.Text = "";
            LastNameTextBox.Text = "";
            EmailTextBox.Text = "";
           // Response.Redirect("login.aspx");
        }
    }

    protected void checkUserExist()
    {
        SqlConnection ObjConnection2 = new SqlConnection("Data Source=.;Initial Catalog=UML;Integrated Security=True");
        ObjConnection2.Open();
        string StringCmnd2 = @"SELECT Registration.Email FROM Registration WHERE Registration.Email = '" + EmailTextBox .Text+ "'";
        SqlCommand SqlCmnd2 = new SqlCommand(StringCmnd2, ObjConnection2);
        SqlDataReader myDataReader2 = SqlCmnd2.ExecuteReader();
        if (myDataReader2.HasRows)
        {
            myDataReader2.Read();
            string myScriptValue = " {sweetAlert('Oops...', 'A User is Already Exist With Email That You Entered!' , 'error');}";
            ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "myScriptName", myScriptValue, true);
            userExist = true;
        }
        ObjConnection2.Close();
    }
    protected void ShowAlert()
    {
        ScriptManager.RegisterStartupScript(this, GetType(), "displayalertmessage", "ShowAlertBox()", true);

    }
}
