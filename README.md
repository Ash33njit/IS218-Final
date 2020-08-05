# •	Feature 1
Create a login and registration process that includes email verification.  You can use a service like SendGrid to send email and you should look for a Flask Plugin to help.

## app.py code for feature 1
### added email.html for for while also editing the init.sql file to add an email table. 

```@app.route('/email/new', methods=['GET'])
def form_insert_email_get():
    return render_template('email.html', title='Register' Form')


@app.route('/email/<_email>', method=['GET'])
def send_email(_email):
    mail.send_email(
        from_email='ash33@njit.edu',
        to_email=_email,
        subject='Test'
        text='Body,'
    )
    return redirect("/", code=302)

@app.route('/email/new', methods=['POST'])
def form_insert_email_post():
    cursor = mysql.get_db().cursor()
    inputData = (request.form.get('fldEmail'), request.form.get('fldPassword'), request.form.get('fldFName'),
                 request.form.get('fldLName')
    sql_insert_query = """INSERT INTO tblEmailImport (fldEmail,fldPassword,fldFName,fldCLName) VALUES (%s, %s,%s, %s) """
    cursor.execute(sql_insert_query, inputData)
    mysql.get_db().commit()
    return redirect("/", code=302)
```

# •	Feature 2
 Create a calendar display and retrieve data out of Google Calendar.   Allow someone to add an even to their Google Calendar and display it on the page.  You can use the HTML full calendar plugin here (Links to an external site.) and you can probably make an iCal Feed from your Google calendar to feed into it, but you will need to cache the data locally in the database and update the data periodically between each request is made.  For example, if the calendar data has not been updated in 5 minutes, make a request to retrieve the data and update the database and then display that data in the fullCalendar page.