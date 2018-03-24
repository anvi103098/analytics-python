import mysql.connector as conn
User = "root"
Name = "portfolio"
Host = "localhost"
password = "password"
"""
Do Not Change!!
Copyrighted by the edX course "https://courses.edx.org/courses/course-v1:ColumbiaX+BAMM.101x+1T2018/course/"

"""
db = conn.connect(host = Host, user = User, password = password, database = Name )
cursor = db.cursor()

file = "startercode.0/portfolio.txt"
with open(file,'r') as f:
    line_count = 0
    stocks_set = set()
    for line in f:
        line = line.strip()

        if line_count == 0:
            headers = line.split(':')
            headers = [x.replace(' ','_') for x in headers]
            query1 = "DROP TABLE IF EXISTS stocks;"
            query2 = "DROP TABLE IF EXISTS holdings"
            cursor.execute(query1)
            cursor.execute(query2)
            query1 = "CREATE TABLE IF NOT EXISTS stocks ("
            query1 += headers[0] + " VARCHAR(10),"
            query1 += headers[1] + " VARCHAR(30));"
            query2 = "CREATE TABLE IF NOT EXISTS holdings ("
            query2 += headers[0] + " VARCHAR(10),"
            query2 += headers[2] + " DECIMAL(10,2),"
            query2 += headers[3] + " INT,"
            query2 += headers[4] + " DATE);"
            cursor.execute(query1)
            cursor.execute(query2)
            line_count += 1
            continue        
        data = line.split(':')
        stock_info = (data[0],data[1])
        stocks_set.add(stock_info)
        holdings_query = 'INSERT INTO holdings VALUES ("'
        holdings_query +=data[0] + '",'
        holdings_query +=data[2] + ','
        holdings_query +=data[3] + ',"'
        holdings_query +=data[4] + '");'
        cursor.execute(holdings_query)
for s_info in stocks_set:
    stock_query = 'INSERT INTO stocks VALUES ("'
    stock_query += s_info[0] + '","'
    stock_query += s_info[1] +'");'
    cursor.execute(stock_query)
db.commit()
db.close()
