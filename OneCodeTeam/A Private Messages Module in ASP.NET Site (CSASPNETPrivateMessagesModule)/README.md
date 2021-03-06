# A Private Messages Module in ASP.NET Site (CSASPNETPrivateMessagesModule)
## Requires
- Visual Studio 2010
## License
- MS-LPL
## Technologies
- ASP.NET
## Topics
- Module
## Updated
- 12/12/2012
## Description

<h1>A Private Messaging Module in ASP.NET Site (CSASPNETPrivateMessagesModule)</h1>
<h2>Introduction </h2>
<p class="MsoNormal">This sample shows how to create a private messaging module in an ASP.NET site. This module can
<a name="OLE_LINK3"></a><a name="OLE_LINK2"><span style="">base on </span></a>the ASP.NET Membership or other member systems. And it can be easily added to an existing ASP.NET Site.</p>
<h2>Running the Sample</h2>
<p class="MsoNormal">Please follow these demonstration steps below.</p>
<p class="MsoNormal">Step 1:&nbsp;Open the <span style="">CSASPNETPrivateMessagesModule</span>.sln. Expand the
<a name="OLE_LINK1"><span style="">CSASPNETPrivateMessagesModule</span> </a>web application.<span style=""> Right click CreateUser.aspx and choose &quot;View in Browser&quot; to create some test accounts.</span><span style="font-size:9.5pt; line-height:115%; font-family:Consolas"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style=""></span></p>
<p class="MsoNormal">Step 2:<span style="">&nbsp; </span>Press Ctrl &#43; F5 to show the Default.aspx then login.</p>
<p class="MsoNormal"><span style=""><img src="72461-image.png" alt="" width="751" height="498" align="middle">
</span></p>
<p class="MsoNormal">Select message recipient then click the button &quot;Add to list&quot;.
</p>
<p class="MsoNormal"><span style=""><img src="72462-image.png" alt="" width="512" height="328" align="middle">
</span></p>
<p class="MsoNormal">After typing the content and title, you can click the &quot;Send/Save Draft&quot; button to send/save the message.</p>
<p class="MsoNormal">Step 3:<span style="">&nbsp;&nbsp; </span>Click the link of &quot;Draft&quot;, &quot;Inbox&quot; or &quot;OutBox&quot;.<br>
<span style=""><img src="72463-image.png" alt="" width="548" height="380" align="middle">
</span></p>
<p class="MsoNormal">Click the detail link.</p>
<p class="MsoNormal"><span style=""><img src="72464-image.png" alt="" width="445" height="192" align="middle">
</span></p>
<p class="MsoNormal">Click reply or reply all.</p>
<p class="MsoNormal"><span style=""><img src="72465-image.png" alt="" width="535" height="339" align="middle">
</span></p>
<p class="MsoNormal">Reply or save draft.<br>
Step 4:<span style="">&nbsp;&nbsp; </span>Login with other account to receive the message.</p>
<p class="MsoNormal">Step 5:<span style="">&nbsp;&nbsp; </span>Validation finished.</p>
<h2>Using the Code</h2>
<p class="MsoNormal" style="">Code Logical: </p>
<p class="MsoNormal">Step 1. Create a new database in SQL Server. Name it as &quot;<span style="">MembershipProviderTest</span>&quot;.
<span style="">&nbsp;&nbsp; </span></p>
<p class="MsoNormal">Step 2. Use the command-line tool aspnet_regsql.exe (located in the Framework folder) to create the tables and procedures used by the
<span style="">Membership Provider</span>.</p>
<p class="MsoNormal" style="">Create a table for message, in this sample it is MessageTable. The definition of the message table as shown below:</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>SQL</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">mysql</span>

<pre id="codePreview" class="mysql">
CREATE TABLE [dbo].[MessageTable](
    [MessageID] [int] IDENTITY(1,1) NOT NULL,
    [FromUserId] [uniqueidentifier] NULL,
    [ToUserId] [uniqueidentifier] NULL,
    [Message] [nvarchar](200),
    [MessageTitle] [nvarchar](50),
    [CreateDate] [datetime] NOT NULL,
    [State] [tinyint] NULL
)

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal">Step 3. Create a C# &quot;ASP.NET Web Application&quot; in Visual Studio 20<span style="">10</span>. Name it as &quot;<span style="">CSASPNETPrivateMessagesModule</span>&quot;.
</p>
<p class="MsoNormal">Step 4. Add a master page. It is used to uniform page style and navigation. Use the master to create six Pages then rename them to &quot;CreateUser.aspx&quot;,&quot; Login.aspx&quot;,<br>
&quot;MessageList.aspx&quot;,&quot;<span style=""> <span style="color:black">itemdetail.aspx</span></span>&quot;,&quot;newitem.aspx&quot; and &quot;Default.aspx&quot;.<span style="">&nbsp;
</span>Add a CreateUserWizard Control to the CreateUser page, the code as shown below:</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>HTML</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">html</span>

<pre id="codePreview" class="html">
&lt;asp:CreateUserWizard ID=&quot;CreateUserWizard1&quot; runat=&quot;server&quot; ActiveStepIndex=&quot;0&quot; ContinueDestinationPageUrl=&quot;~/Default.aspx&quot;&gt;
       &lt;WizardSteps&gt;
         &lt;asp:CreateUserWizardStep ID=&quot;CreateUserWizardStep1&quot; runat=&quot;server&quot;&gt;
         &lt;/asp:CreateUserWizardStep&gt;
         &lt;asp:CompleteWizardStep ID=&quot;CompleteWizardStep1&quot; runat=&quot;server&quot;&gt;
         &lt;/asp:CompleteWizardStep&gt;
       &lt;/WizardSteps&gt;
     &lt;/asp:CreateUserWizard&gt;

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>Add a <span style="">Login Control to the Login page, the code as shown below:
</span></p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>HTML</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">html</span>

<pre id="codePreview" class="html">
&lt;asp:Login ID=&quot;Login1&quot; runat=&quot;server&quot;&gt;
  &lt;/asp:Login&gt;

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal">Step 5.<span style="">&nbsp; </span>Now, begin to edit the web.config.</p>
<p class="MsoNormal">First, configure the Connection Strings as follows; <span style="">
you can try the </span>connectionString1 <span style="">or </span>connectionString<span style="">2.
</span></p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>XML</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">xml</span>

<pre id="codePreview" class="xml">
&lt;connectionStrings&gt;
   &lt;!-- Clear the default connection. --&gt;
   &lt;clear/&gt;
   &lt;!-- Connect to the database in the App_Data folder --&gt;
   &lt;add name=&quot;LocalSqlServer&quot; providerName=&quot;System.Data.SqlClient&quot; connectionString=&quot;Data Source=.\SQLExpress;Integrated Security=True;User Instance=True;AttachDBFilename=|DataDirectory|MembershipProviderTest.mdf&quot;/&gt;
   &lt;!-- Connect to the database which has been attached to the database manager. --&gt;
   &lt;!--&lt;add name=&quot;LocalSqlServer&quot; connectionString=&quot;Data Source=.;Initial Catalog=D:\PROJECTDIR\NET\CSASPNETMEMBERSHIPPROVIDER\VBASPNETMEMBERSHIPPROVIDER\APP_DATA\MEMBERSHIPPROVIDERTEST.MDF;Integrated Security=True&quot;/&gt;--&gt;
 &lt;/connectionStrings&gt;

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal"><br>
Second, configure the CreateUser pa<span style="">ge and </span><span style="">the
</span><span style="">security authentication mode:</span><span style=""> </span>
</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>XML</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">xml</span>

<pre id="codePreview" class="xml">
&lt;location path=&quot;CreateUser.aspx&quot;&gt;
   &lt;system.web&gt;
     &lt;authorization&gt;
       &lt;allow users=&quot;?&quot;/&gt;
     &lt;/authorization&gt;
   &lt;/system.web&gt;
 &lt;/location&gt;
&lt;authentication mode=&quot;Forms&quot;&gt;
       &lt;forms loginUrl=&quot;login.aspx&quot; name=&quot;.ASPXFORMSAUTH&quot;/&gt;
     &lt;/authentication&gt;
     &lt;authorization&gt;
       &lt;deny users=&quot;?&quot;/&gt;
     &lt;/authorization&gt;

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal"><span style="">&nbsp;</span>Finally, configure the membership<span style=""> to
</span>AspNetSqlMembershipProvider<span style="">:</span><span style=""> </span></p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>XML</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">xml</span>

<pre id="codePreview" class="xml">
&lt;!--Build-in Provider Configuration--&gt;
     &lt;membership defaultProvider=&quot;AspNetSqlMembershipProvider&quot; userIsOnlineTimeWindow=&quot;15&quot;&gt;
       &lt;providers&gt;
       &lt;/providers&gt;
     &lt;/membership&gt;

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal">Step <span style="">6</span>. Create the helper class.</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">csharp</span>

<pre id="codePreview" class="csharp">
// Sql connection.
   public static string connetionString = ConfigurationManager.ConnectionStrings[&quot;LocalSqlServer&quot;].ConnectionString;    


   /// &lt;summary&gt;
   /// Get UserName By ProviderUserKey
   /// &lt;/summary&gt;
   /// &lt;param name=&quot;id&quot;&gt;ProviderUserKey&lt;/param&gt;
   /// &lt;returns&gt;UserName&lt;/returns&gt;
   public static string getUserNameByProviderUserKey(string id)
   {
       // UserName
       string strName = string.Empty;


       // Query string
       string queryString = &quot;SELECT UserName FROM [aspnet_Users] where UserID=@id&quot;;


       #region database Operation
       using (SqlConnection connection = new SqlConnection(connetionString))
       {
           SqlCommand command = new SqlCommand(queryString, connection);
           SqlParameter para2 = new SqlParameter(&quot;id&quot;, id);
           command.Parameters.Add(para2);
           connection.Open();
           SqlDataReader reader = command.ExecuteReader();
           if (reader.HasRows)
           {
               reader.Read();
               strName = reader[0].ToString();
           }
           reader.Close();
           connection.Close();
       }
       #endregion


       return strName;
   }


   /// &lt;summary&gt;
   /// Get ProviderUserKey By UserName
   /// &lt;/summary&gt;
   /// &lt;param name=&quot;strName&quot;&gt;UserName&lt;/param&gt;
   /// &lt;returns&gt;ProviderUserKey&lt;/returns&gt;
   public static string getUserKeyByUserName(string strName)
   {
       // ProviderUserKey
       string strUserKey = string.Empty;


       // Query string
       string queryString = &quot;SELECT UserID FROM [aspnet_Users] where UserName=@Name&quot;;


       #region database Operation
       using (SqlConnection connection = new SqlConnection(connetionString))
       {
           SqlCommand command = new SqlCommand(queryString, connection);
           SqlParameter para2 = new SqlParameter(&quot;Name&quot;, strName);
           command.Parameters.Add(para2);
           connection.Open();
           SqlDataReader reader = command.ExecuteReader();
           if (reader.HasRows)
           {
               reader.Read();
               strUserKey = reader[0].ToString();
           }
           reader.Close();
           connection.Close();
       }
       #endregion


       return strUserKey;
   }

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal">Step <span style="">7</span>. The code of list page as shown below:</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">csharp</span>

<pre id="codePreview" class="csharp">
protected void Page_Load(object sender, EventArgs e)
       {
           MembershipUser currentUser = Membership.GetUser();// Current User          


           string strFlag = Request.QueryString[&quot;flag&quot;];
           if (!IsPostBack)
           {
               // Query string
               string queryString = &quot;SELECT [MessageID], [FromUserId], [ToUserId], [Message], &quot;
                   &#43; &quot;[CreateDate], [MessageTitle], [State] FROM [MessageTable]&quot;;


               // The status field has two values, the normal message is 1 while a draft is 0.
               switch (strFlag)
               {
                   case &quot;0&quot;: // Draft
                       queryString &#43;= &quot; where state=0 and FromUserId=@UserId&quot;;
                       break;
                   case &quot;1&quot;: // Inbox
                       queryString &#43;= &quot; where state=1 and ToUserId=@UserId&quot;;
                       break;
                   case &quot;2&quot;: // Outbox
                       queryString &#43;= &quot; where state=1 and FromUserId=@UserId&quot;;
                       break;
                   default:
                       break;
               }


               if (!string.IsNullOrEmpty(strFlag))
               {
                   SqlDataAdapter adapter = new SqlDataAdapter();
                   DataSet sqlData = new DataSet();


                   using (SqlConnection connection = new SqlConnection(Common.connetionString))
                   {
                       // Set query string
                       adapter.SelectCommand = new SqlCommand(queryString, connection);
                       SqlParameter para = new SqlParameter(&quot;UserId&quot;, currentUser.ProviderUserKey);
                       adapter.SelectCommand.Parameters.Add(para);


                       // Open connection
                       connection.Open();


                       // Sql data is stored DataSet.
                       adapter.Fill(sqlData, &quot;MessageTable&quot;);


                       // Close connection
                       connection.Close();
                   }


                   // Bind datatable to GridView
                   gdvView.DataSource = sqlData.Tables[0];
                   gdvView.DataBind();
               }
           }
       }

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal">Step <span style="">8</span>. The code of detail page as shown below:</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">csharp</span>

<pre id="codePreview" class="csharp">
protected void Page_Load(object sender, EventArgs e)
        {
            MembershipUser currentUser;     // Current User
            currentUser = Membership.GetUser();


            if (!string.IsNullOrEmpty(Request.QueryString[&quot;ID&quot;]))
            {
                id = Convert.ToInt32(Request.QueryString[&quot;ID&quot;]);


                // Query string
                string queryString = &quot;SELECT [MessageID], [FromUserId], [ToUserId], [Message], &quot;
                    &#43; &quot;[CreateDate], [MessageTitle], [State] FROM [MessageTable] &quot;
                    &#43; &quot; where MessageID=@id and (ToUserId=@userid or FromUserId=@userid)&quot;;


                using (SqlConnection connection = new SqlConnection(Common.connetionString))
                {
                    // sql command
                    SqlCommand command = new SqlCommand(queryString, connection);


                    #region BasicInfo
                    SqlParameter para1 = new SqlParameter(&quot;id&quot;, id);
                    SqlParameter para2 = new SqlParameter(&quot;userId&quot;, currentUser.ProviderUserKey);
                    command.Parameters.Add(para1);
                    command.Parameters.Add(para2);
                    connection.Open();
                    SqlDataReader reader = command.ExecuteReader();
                    if (reader.HasRows)
                    {
                        reader.Read();
                        strFrom = reader[&quot;FromUserId&quot;].ToString();
                        strTitle = reader[&quot;MessageTitle&quot;].ToString();
                        strContent = reader[&quot;Message&quot;].ToString();
                        strTime = reader[&quot;CreateDate&quot;].ToString();


                    }
                    reader.Close();
                    #endregion


                    #region Get the recipients
                    queryString = &quot;SELECT ToUserId FROM MessageTable where CreateDate = @CreateDate&quot;
                        &#43; &quot; AND FromUserId = @FromUserId&quot;;
                    para1 = new SqlParameter(&quot;CreateDate&quot;, Convert.ToDateTime(strTime));
                    para2 = new SqlParameter(&quot;FromUserId&quot;, (object)strFrom);
                    command.Parameters.Clear();
                    command.CommandText = queryString;
                    command.Parameters.Add(para1);
                    command.Parameters.Add(para2);
                    reader = command.ExecuteReader();
                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            strTo &#43;= &quot;;&quot; &#43; Common.getUserNameByProviderUserKey(reader[0].ToString());
                        }
                    }
                    if (strTo.Length &gt; 0)
                    {
                        strTo = strTo.Substring(1);
                    }
                    reader.Close();
                    #endregion


                    connection.Close();
                }
            }


            #region bind to control
            ltrContent.Text = strContent;
            ltrFrom.Text = Common.getUserNameByProviderUserKey(strFrom);
            ltrTo.Text = strTo;
            ltrTime.Text = strTime;
            ltrTitle.Text = strTitle;
            #endregion
        }


        protected void btnReply_Click(object sender, EventArgs e)
        {
            Response.Redirect(&quot;NewItem.aspx?flag=1&rid=&quot; &#43; id);
        }


        protected void btnReplyAll_Click(object sender, EventArgs e)
        {
            Response.Redirect(&quot;NewItem.aspx?flag=2&rid=&quot; &#43; id);
        }

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal">Step <span style="">9.</span> The code of new item page as shown below:</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">csharp</span>

<pre id="codePreview" class="csharp">
protected void Page_Load(object sender, EventArgs e)
        {
            if (!string.IsNullOrEmpty(Request.QueryString[&quot;rid&quot;]))
            {
                rid = Convert.ToInt32(Request.QueryString[&quot;rid&quot;]);


                // The flag of reply and reply all.
                string flag = Request.QueryString[&quot;flag&quot;];


                // According to the flag, get the recipient list
                switch (flag)
                {
                    case &quot;1&quot;:   // reply
                        GetBasicInfo();
                        strTo = Common.getUserNameByProviderUserKey(strFrom);
                        break;
                    case &quot;2&quot;:   // replyall
                        GetBasicInfo();
                        GetReplyAllTo();
                        break;
                    default:
                        break;
                }


                strContent = &quot;From: &quot; &#43; Common.getUserNameByProviderUserKey(strFrom)
                    &#43; &quot;\nSent: &quot; &#43; strTime
                    &#43; &quot;\nTo: &quot; &#43; strTo
                    &#43; &quot;\nTitle: &quot; &#43; strTitle
                    &#43; &quot;\nContent: &quot; &#43; strContent;


                strTitle = &quot;Re:&quot; &#43; strTitle;
            }


            if (!IsPostBack)
            {
                BindUser();


                #region bind to control
                txtContent.Text = strContent;
                txtTo.Text = strTo;
                txtTitle.Text = strTitle;
                #endregion
            }
        }


        /// &lt;summary&gt;
        /// Get recipient list of reply all
        /// &lt;/summary&gt;
        private void GetReplyAllTo()
        {
            using (SqlConnection connection = new SqlConnection(Common.connetionString))
            {
                queryString = &quot;SELECT ToUserId from MessageTable where CreateDate=@create and FromUserId=@FromUserId&quot;;
                command = new SqlCommand(queryString, connection);
                para1 = new SqlParameter(&quot;create&quot;, strTime);
                para2 = new SqlParameter(&quot;FromUserId&quot;, strFrom);
                command.Parameters.Clear();
                command.CommandText = queryString;
                command.Parameters.Add(para1);
                command.Parameters.Add(para2);


                connection.Open();
                reader = command.ExecuteReader();
                if (reader.HasRows)
                {
                    while (reader.Read())
                    {
                        strTo &#43;= &quot;;&quot; &#43; Common.getUserNameByProviderUserKey(reader[0].ToString());
                    }
                }
                if (strTo.Length &gt; 0)
                {
                    strTo = strTo.Substring(1);
                }
                reader.Close();
                connection.Close();
            }
        }


        /// &lt;summary&gt;
        /// Get the basic infomation of the message
        /// &lt;/summary&gt;
        private void GetBasicInfo()
        {
            MembershipUser currentUser; // Current User
            currentUser = Membership.GetUser();


            // Query string
            queryString = &quot;SELECT [MessageID], [FromUserId], [ToUserId], [Message], [CreateDate],&quot;
                &#43; &quot; [MessageTitle], [State] FROM [MessageTable] &quot;
                &#43; &quot;where MessageID=@id and (ToUserId=@userid or FromUserId=@userid)&quot;;
            using (SqlConnection connection = new SqlConnection(Common.connetionString))
            {
                command = new SqlCommand(queryString, connection);
                para1 = new SqlParameter(&quot;id&quot;, rid);
                para2 = new SqlParameter(&quot;userId&quot;, currentUser.ProviderUserKey);
                command.Parameters.Add(para1);
                command.Parameters.Add(para2);
                connection.Open();
                reader = command.ExecuteReader();
                if (reader.HasRows)
                {
                    reader.Read();
                    strFrom = reader[&quot;FromUserId&quot;].ToString();
                    strTitle = reader[&quot;MessageTitle&quot;].ToString();
                    strContent = reader[&quot;Message&quot;].ToString();
                    strTime = reader[&quot;CreateDate&quot;].ToString();
                }
                reader.Close();
                connection.Close();
            }
        }


        /// &lt;summary&gt;
        /// Get all MembershipUser
        /// &lt;/summary&gt;
        private void BindUser()
        {
            MembershipUserCollection muc = Membership.GetAllUsers();
            chlUser.DataSource = muc;
            chlUser.DataBind();
        }


        protected void btnAdd_Click(object sender, EventArgs e)
        {
            string strTo = string.Empty;


            // Loop the users and add the selected user to recipient list
            foreach (ListItem item in this.chlUser.Items)
            {
                if (item.Selected)
                {
                    strTo &#43;= &quot;;&quot; &#43; item.Text;
                }
            }


            if (strTo.Length &gt; 0)
            {
                txtTo.Text = strTo.Substring(1);
            }
        }


        // Send message
        protected void btnEnter_Click(object sender, EventArgs e)
        {
            if (IsValid)
            {
                SaveToDB();
            }
        }


        /// &lt;summary&gt;
        /// Save the message to Database 
        /// &lt;/summary&gt;
        private void SaveToDB()
        {
            string strSql = &quot;&quot;;
            // Get recipient list
            string[] tos = txtTo.Text.Split(';');


            // Save message for everyone in the recipient list
            for (int i = 0; i &lt; tos.Length; i&#43;&#43;)
            {
                strSql &#43;= &quot;insert into MessageTable(FromUserId,ToUserId,Message,MessageTitle,CreateDate,state)&quot;
                    &#43; &quot; values('&quot; &#43; Membership.GetUser().ProviderUserKey &#43; &quot;','&quot;
                    &#43; Common.getUserKeyByUserName(tos[i]) &#43; &quot;','&quot; &#43; txtContent.Text.Trim()
                    &#43; &quot;','&quot; &#43; txtTitle.Text.Trim() &#43; &quot;','&quot; &#43; DateTime.Now.ToString() &#43; &quot;',&quot; &#43; state &#43; &quot;);&quot;;
            }


            using (SqlConnection connection = new SqlConnection(Common.connetionString))
            {
                connection.Open();
                SqlTransaction tran = connection.BeginTransaction();
                try
                {


                    SqlCommand cmd = new SqlCommand(strSql, connection, tran);
                    cmd.ExecuteNonQuery();
                    tran.Commit();
                }
                catch (Exception e)
                {
                    tran.Rollback();
                }
                finally
                {
                    connection.Close();
                    Response.Redirect(&quot;messagelist.aspx?flag=2&quot;);
                }
            }
        }


        /// &lt;summary&gt;
        /// Save draft
        /// &lt;/summary&gt;
        /// &lt;param name=&quot;sender&quot;&gt;&lt;/param&gt;
        /// &lt;param name=&quot;e&quot;&gt;&lt;/param&gt;
        protected void btnDraft_Click(object sender, EventArgs e)
        {
            state = 0; // This is the value of draft
            SaveToDB();
        }

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal"><span class="GramE">Step <span style="">10</span>.</span> Build the application<span style="">,</span> and then it can be debugged.</p>
<h2>More Information</h2>
<p class="MsoNormal">SqlMembershipProvider Class<br>
<a href="http://msdn.microsoft.com/en-us/library/system.web.security.sqlmembershipprovider.aspx">http://msdn.microsoft.com/en-us/library/system.web.security.sqlmembershipprovider.aspx</a><br>
Membership Class<br>
<a href="http://msdn.microsoft.com/en-us/library/system.web.security.membership.aspx">http://msdn.microsoft.com/en-us/library/system.web.security.membership.aspx</a></p>
<hr>
<div><a href="http://go.microsoft.com/?linkid=9759640" style="margin-top:3px"><img alt="" src="http://bit.ly/onecodelogo">
</a></div>
