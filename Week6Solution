User = "root"
Name = "portfolio"
Host = "localhost"
password = "password"

def get_price(ticker):
    import requests
    from bs4 import BeautifulSoup
    #from decimal import Decimal

    filename="startercode.0/" + ticker + ".htm"
    #print (filename)
    with open(filename, 'r') as f:
        response_page = BeautifulSoup(f, 'lxml')
        div_tag = response_page.find('div',id="price-panel")
        price = div_tag.find('span', class_='pr').getText().strip()
        if not price:
            print ("Cannot find Price")
             
    #print (price.replace(",", ""))
    return float(price.replace(",", ""))

def get_pnl():
    import mysql.connector as conn
    from decimal import Decimal
    
    db = conn.connect(host = Host, user = User, password = password, database = Name )
    cursor = db.cursor()
    gain_dict = dict()
    
    queryCompanyName = "select *  from stocks"
    cursor.execute(queryCompanyName)
    companyList = cursor.fetchall()
    #print (companyList)
    for row in companyList:
        #ticker = row[0]
        #companyName = row[1]
        
        #retrieving the total value of each ticker from the database
        queryPurchasePrice = "select Purchase_Price, Shares from holdings where ticker = '" + row[0] + "'"
        cursor.execute(queryPurchasePrice)
        holdingsRow =  cursor.fetchall()
        #print (holdingsRow)
        purchasedValues = sum([a * b for a,b in holdingsRow])
        purchasedShares = sum([x[1] for x in holdingsRow])
        #print (purchasedShares)
        #print(purchasedValues)
        
        newPrice = get_price(row[0])
        #print (newPrice)
        #print (type (purchasedValues))
        #print (type (Decimal(newPrice*purchasedShares)))
        netPrice = abs(Decimal(newPrice*purchasedShares)-purchasedValues)
        
        #print (row[0] + " " + row[1] + " " + str(purchasedValues) + " " + str(netPrice))


        gain_dict[row[1]] = float(netPrice)
        
    
    cursor.close()
    return gain_dict

get_pnl()
